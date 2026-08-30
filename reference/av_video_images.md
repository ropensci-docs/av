# Convert video to images

Splits a video file in a set of image files. Default image format is
jpeg which has good speed and compression. Use `format = "png"` for
losless images.

## Usage

``` r
av_video_images(
  video,
  destdir = tempfile(),
  format = "jpg",
  fps = NULL,
  trim = NULL
)
```

## Arguments

- video:

  an input video

- destdir:

  directory where to save the png files

- format:

  image format such as `png` or `jpeg`, must be available from
  [`av_encoders()`](https://docs.ropensci.org/av/reference/formats.md)

- fps:

  sample rate of images. Use `NULL` to get all images.

- trim:

  string value for [ffmpeg trim
  filter](https://ffmpeg.org/ffmpeg-filters.html#trim) for example
  `"10:15"` for seconds or `"start_frame=100:end_frame=110"` for frames.

## Details

For large input videos you can set fps to sample only a limited number
of images per second. This also works with fractions, for example
`fps = 0.2` will output one image for every 5 sec of video.

## Examples

``` r
if (FALSE) { # \dontrun{
curl::curl_download('https://jeroen.github.io/images/blackbear.mp4', 'blackbear.mp4')
av_video_images('blackbear.mp4', fps = 1, trim = "10:20")
} # }
```
