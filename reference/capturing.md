# Record Video from Graphics Device

Runs the expression and captures all plots into a video. The
av_spectrogram_video function is a wrapper that plots data from
[read_audio_fft](https://docs.ropensci.org/av/reference/read_audio.md)
with a moving bar and background audio.

## Usage

``` r
av_capture_graphics(
  expr,
  output = "output.mp4",
  width = 720,
  height = 480,
  framerate = 1,
  vfilter = "null",
  audio = NULL,
  verbose = TRUE,
  ...
)

av_spectrogram_video(
  audio,
  output = "output.mp4",
  framerate = 25,
  verbose = interactive(),
  ...
)
```

## Arguments

- expr:

  an R expression that generates the graphics to capture

- output:

  name of the output file. File extension must correspond to a known
  container format such as `mp4`, `mkv`, `mov`, or `flv`.

- width:

  width in pixels of the graphics device

- height:

  height in pixels of the graphics device

- framerate:

  video framerate in frames per seconds. This is the input fps, the
  output fps may be different if you specify a filter that modifies
  speed or interpolates frames.

- vfilter:

  a string defining an ffmpeg filter graph. This is the same parameter
  as the `-vf` argument in the `ffmpeg` command line utility.

- audio:

  path to media file with audio stream

- verbose:

  emit some output and a progress meter counting processed images. Must
  be `TRUE` or `FALSE` or an integer with a valid
  [av_log_level](https://docs.ropensci.org/av/reference/logging.md).

- ...:

  extra graphics parameters passed to
  [`png()`](https://rdrr.io/r/grDevices/png.html)

## See also

Other av: [`demo()`](https://docs.ropensci.org/av/reference/demo.md),
[`encoding`](https://docs.ropensci.org/av/reference/encoding.md),
[`formats`](https://docs.ropensci.org/av/reference/formats.md),
[`info`](https://docs.ropensci.org/av/reference/info.md),
[`logging`](https://docs.ropensci.org/av/reference/logging.md),
[`read_audio_fft()`](https://docs.ropensci.org/av/reference/read_audio.md)

## Examples

``` r
# \donttest{
library(gapminder)
library(ggplot2)
makeplot <- function(){
  datalist <- split(gapminder, gapminder$year)
  lapply(datalist, function(data){
    p <- ggplot(data, aes(gdpPercap, lifeExp, size = pop, color = continent)) +
      scale_size("population", limits = range(gapminder$pop)) + geom_point() + ylim(20, 90) +
      scale_x_log10(limits = range(gapminder$gdpPercap)) + ggtitle(data$year) + theme_classic()
    print(p)
  })
}

# Play 1 plot per sec, and use an interpolation filter to convert into 10 fps
video_file <- file.path(tempdir(), 'output.mp4')
av_capture_graphics(makeplot(), video_file, 1280, 720, res = 144, vfilter = 'framerate=fps=10')
#> [1] "/tmp/RtmpS6W2dK/output.mp4"
av::av_media_info(video_file)
#> $duration
#> [1] 12.9
#> 
#> $video
#>   width height codec frames framerate  format
#> 1  1280    720  h264    130        10 yuv420p
#> 
#> $audio
#> NULL
#> 
# utils::browseURL(video_file)# }
```
