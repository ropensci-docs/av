# AV Formats

List supported filters, codecs and container formats.

## Usage

``` r
av_encoders()

av_decoders()

av_filters()

av_muxers()

av_demuxers()
```

## Details

Encoders and decoders convert between raw video/audio frames and
compressed stream data for storage or transfer. However such a
compressed data stream by itself does not constitute a valid video
format yet. Muxers are needed to interleave one or more
audio/video/subtitle streams, along with timestamps, metadata, etc, into
a proper file format, such as mp4 or mkv.

Conversely, demuxers are needed to read a file format into the separate
data streams for subsequent decoding into raw audio/video frames. Most
operating systems natively support demuxing and decoding common formats
and codecs, needed to play those videos. However for encoding and muxing
such videos, ffmpeg must have been configured with specific external
libraries for a given codec or format.

## See also

Other av:
[`capturing`](https://docs.ropensci.org/av/reference/capturing.md),
[`demo()`](https://docs.ropensci.org/av/reference/demo.md),
[`encoding`](https://docs.ropensci.org/av/reference/encoding.md),
[`info`](https://docs.ropensci.org/av/reference/info.md),
[`logging`](https://docs.ropensci.org/av/reference/logging.md),
[`read_audio_fft()`](https://docs.ropensci.org/av/reference/read_audio.md)
