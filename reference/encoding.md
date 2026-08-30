# Encode or Convert Audio / Video

Encodes a set of images into a video, using custom container format,
codec, fps, [video
filters](https://ffmpeg.org/ffmpeg-filters.html#Video-Filters), and
audio track. If input contains video files, this effectively combines
and converts them to the specified output format.

## Usage

``` r
av_encode_video(
  input,
  output = "output.mp4",
  framerate = 24,
  vfilter = "null",
  codec = NULL,
  audio = NULL,
  verbose = TRUE
)

av_video_convert(video, output = "output.mp4", verbose = TRUE)

av_audio_convert(
  audio,
  output = "output.mp3",
  format = NULL,
  channels = NULL,
  sample_rate = NULL,
  bit_rate = NULL,
  start_time = NULL,
  total_time = NULL,
  verbose = interactive()
)
```

## Arguments

- input:

  a vector with image or video files. A video input file is treated as a
  series of images. All input files should have the same width and
  height.

- output:

  name of the output file. File extension must correspond to a known
  container format such as `mp4`, `mkv`, `mov`, or `flv`.

- framerate:

  video framerate in frames per seconds. This is the input fps, the
  output fps may be different if you specify a filter that modifies
  speed or interpolates frames.

- vfilter:

  a string defining an ffmpeg filter graph. This is the same parameter
  as the `-vf` argument in the `ffmpeg` command line utility.

- codec:

  name of the video codec as listed in
  [av_encoders](https://docs.ropensci.org/av/reference/formats.md). The
  default is `libx264` for most formats, which usually the best choice.

- audio:

  audio or video input file with sound for the output video

- verbose:

  emit some output and a progress meter counting processed images. Must
  be `TRUE` or `FALSE` or an integer with a valid
  [av_log_level](https://docs.ropensci.org/av/reference/logging.md).

- video:

  input video file with optionally also an audio track

- format:

  a valid output format name from the list of
  [`av_muxers()`](https://docs.ropensci.org/av/reference/formats.md).
  Default `NULL` infers format from the file extension.

- channels:

  number of output channels. Default `NULL` will match input.

- sample_rate:

  output sampling rate. Default `NULL` will match input.

- bit_rate:

  output bitrate (quality). A common value is 192000. Default `NULL`
  will match input.

- start_time:

  number greater than 0, seeks in the input file to position.

- total_time:

  approximate number of seconds at which to limit the duration of the
  output file.

## Details

The target container format and audio/video codes are automatically
determined from the file extension of the output file, for example
`mp4`, `mkv`, `mov`, or `flv`. For video output, most systems also
support `gif` output, but the compression~quality for gif is really bad.
The [gifski](https://cran.r-project.org/package=gifski) package is
better suited for generating animated gif files. Still using a proper
video format is results in much better quality.

It is recommended to use let ffmpeg choose the suitable codec for a
given container format. Most video formats default to the `libx264`
video codec which has excellent compression and works on all modern
browsers, operating systems, and digital TVs.

To convert from/to raw PCM audio, use file extensions `".ub"` or `".sb"`
for 8bit unsigned or signed respectively, or `".uw"` or `".sw"` for
16-bit, see `extensions` in
[`av_muxers()`](https://docs.ropensci.org/av/reference/formats.md).
Alternatively can also convert to other raw audio PCM by setting for
example `format = "u16le"` (i.e. unsigned 16-bit little-endian) or
another option from the `name` column in
[`av_muxers()`](https://docs.ropensci.org/av/reference/formats.md).

It is safe to interrupt the encoding process by pressing CTRL+C, or via
[setTimeLimit](https://rdrr.io/r/base/setTimeLimit.html). When the
encoding is interrupted, the output stream is properly finalized and all
open files and resources are properly closed.

## See also

Other av:
[`capturing`](https://docs.ropensci.org/av/reference/capturing.md),
[`demo()`](https://docs.ropensci.org/av/reference/demo.md),
[`formats`](https://docs.ropensci.org/av/reference/formats.md),
[`info`](https://docs.ropensci.org/av/reference/info.md),
[`logging`](https://docs.ropensci.org/av/reference/logging.md),
[`read_audio_fft()`](https://docs.ropensci.org/av/reference/read_audio.md)
