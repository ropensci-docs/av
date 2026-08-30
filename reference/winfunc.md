# Window functions

Several common [windows
function](https://en.wikipedia.org/wiki/Window_function) generators. The
functions return a vector of weights to use in
[read_audio_fft](https://docs.ropensci.org/av/reference/read_audio.md).

## Usage

``` r
hanning(n)

hamming(n)

blackman(n)

bartlett(n)

welch(n)

flattop(n)

bharris(n)

bnuttall(n)

sine(n)

nuttall(n)

bhann(n)

lanczos(n)

gauss(n)

tukey(n)

dolph(n)

cauchy(n)

parzen(n)

bohman(n)
```

## Arguments

- n:

  size of the window (number of weights to generate)

## Examples

``` r
# Window functions
plot(hanning(1024), type = 'l', xlab = 'window', ylab = 'weight')
lines(hamming(1024), type = 'l', col = 'red')
lines(bartlett(1024), type = 'l', col = 'blue')
lines(welch(1024), type = 'l', col = 'purple')
lines(flattop(1024), type = 'l', col = 'darkgreen')
```
