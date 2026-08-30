# Demo Video

Generates random video for testing purposes.

## Usage

``` r
av_demo(
  output = "demo.mp4",
  width = 960,
  height = 720,
  framerate = 5,
  verbose = TRUE,
  ...
)
```

## Arguments

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

- verbose:

  emit some output and a progress meter counting processed images. Must
  be `TRUE` or `FALSE` or an integer with a valid
  [av_log_level](https://docs.ropensci.org/av/reference/logging.md).

- ...:

  other parameters passed to
  [av_capture_graphics](https://docs.ropensci.org/av/reference/capturing.md).

## See also

Other av:
[`capturing`](https://docs.ropensci.org/av/reference/capturing.md),
[`encoding`](https://docs.ropensci.org/av/reference/encoding.md),
[`formats`](https://docs.ropensci.org/av/reference/formats.md),
[`info`](https://docs.ropensci.org/av/reference/info.md),
[`logging`](https://docs.ropensci.org/av/reference/logging.md),
[`read_audio_fft()`](https://docs.ropensci.org/av/reference/read_audio.md)
