# World.JS
このリポジトリは以下の JS ライブラリをビルドしたものです.

https://github.com/YuzukiTsuru/World.JS

上記ライブラリはビルド済みのものが配布されていなかったので,
独自に設置しました.

以下オリジナルのリポジトリからの引用です.

### WavRead_JS

> .wav input functions

```html
<script src="WorldJS.js"></script>

<script>
    let x = Module.WavRead_JS("vaiueo2d.wav");
    console.log(x);
    console.log(x.x);
    console.log(x.fs);
    console.log(x.nbit);
    console.log(x.x_length);
</script>
```

![](.github/ScreenShots/WavRead.png)

##### DIO_JS

> F0 estimation based on DIO (Distributed Inline-filter Operation).

```html
<script src="WorldJS.js"></script>

<script>
    let x = Module.WavRead_JS("vaiueo2d.wav");
    let f0 = Module.Dio_JS(x.x,x.fs,2.0);
    console.log(x);
    console.log(f0);
</script>
```
![Dio](.github/ScreenShots/Dio.png)

##### Harvest_JS

> F0 estimation based on Harvest.

```html
<script src="WorldJS.js"></script>

<script>
    let x = Module.WavRead_JS("vaiueo2d.wav");
    let f0 = Module.Harvest_JS(x.x,x.fs,2.0);
    console.log(x);
    console.log(f0);
</script>
```

##### DisplayInformation

> Display Information

```html
<script src="WorldJS.js"></script>

<script>
    let x = Module.WavRead_JS("vaiueo2d.wav");
    Module.DisplayInformation(x.fs, x.nbit, x.x_length);
</script>
```

##### CheapTrick_JS

> Spectral envelope estimation on the basis of the idea of CheapTrick.

```html
<script src="WorldJS.js"></script>

<script>
    let x = Module.WavRead_JS("vaiueo2d.wav");
    let f0 = Module.Dio_JS(x.x, x.fs, 2.0);
    Module.CheapTrick_JS(x.x, f0.f0, f0.time_axis, x.fs, 2.0);
</script>
```

##### D4C_JS

> Band-aperiodicity estimation on the basis of the idea of D4C.

```html
<script src="WorldJS.js"></script>

<script>
    let x = Module.WavRead_JS("vaiueo2d.wav");
    let f0 = Module.Dio_JS(x.x, x.fs, 2.0);
    let sp = Module.CheapTrick_JS(x.x, f0.f0, f0.time_axis, x.fs, 2.0);
    Module.D4C_JS(x.x, f0.f0, f0.time_axis, sp.fft_size, x.fs, 2.0);
</script>
```

##### Synthesis_JS

> Voice synthesis based on f0, spectrogram and aperiodicity.

```html
<script src="WorldJS.js"></script>

<script>
    let x = Module.WavRead_JS("vaiueo2d.wav");
    let f0 = Module.Dio_JS(x.x, x.fs, 2.0);
    let sp = Module.CheapTrick_JS(x.x, f0.f0, f0.time_axis, x.fs, 2.0);
    let ap = Module.D4C_JS(x.x, f0.f0, f0.time_axis, sp.fft_size, x.fs, 2.0);
    Module.Synthesis_JS(f0.f0, sp.spectral, ap.aperiodicity, sp.fft_size, x.fs, 2.0)
</script>
```

##### WavWrite_JS

> Output Wav File

```html
<script src="WorldJS.js"></script>
<script>
    let x = Module.WavRead_JS("vaiueo2d.wav");
    Module.WavWrite_JS(x.x, x.fs, x.nbit, "out.wav")
</script>
```

## References

[1] M. Morise, F. Yokomori, and K. Ozawa: WORLD: a vocoder-based high-quality speech synthesis system for real-time applications, IEICE transactions on information and systems, vol. E99-D, no. 7, pp. 1877-1884, 2016.
[2] M. Morise: D4C, a band-aperiodicity estimator for high-quality speech synthesis, Speech Communication, vol. 84, pp. 57-65, Nov. 2016. http://www.sciencedirect.com/science/article/pii/S0167639316300413

`In CheapTrick, you can refer the following references.`

[3] M. Morise: CheapTrick, a spectral envelope estimator for high-quality speech synthesis, Speech Communication, vol. 67, pp. 1-7, March 2015. http://www.sciencedirect.com/science/article/pii/S0167639314000697
[4] M. Morise: Error evaluation of an F0-adaptive spectral envelope estimator in robustness against the additive noise and F0 error, IEICE transactions on information and systems, vol. E98-D, no. 7, pp. 1405-1408, July 2015.

`In DIO, you can refer the following reference.`

[5] M. Morise, H. Kawahara and H. Katayose: Fast and reliable F0 estimation method based on the period extraction of vocal fold vibration of singing voice and speech, AES 35th International Conference, CD-ROM Proceeding, Feb. 2009.

`In Harvest, you can refer the following reference.`

[6] M. Morise: Harvest: A high-performance fundamental frequency estimator from speech signals, in Proc. INTERSPEECH 2017, pp. 2321–2325, 2017. http://www.isca-speech.org/archive/Interspeech_2017/abstracts/0068.html

`In the codec of spectral envelope, you can refer the following reference.`

[7] M. Morise, G. Miyashita and K. Ozawa: Low-dimensional representation of spectral envelope without deterioration for full-band speech analysis/synthesis system, in Proc. INTERSPEECH 2017, pp. 409-413, 2017. http://www.isca-speech.org/archive/Interspeech_2017/abstracts/0067.html

`A paper was published to demonstrate that the current version of WORLD was superior to the similar vocoders in the sound quality of re-synthesized speech. This paper also includes the detailed information in the D4C LoveTrain used in the latest version.`

[8] M. Morise and Y. Watanabe: Sound quality comparison among high-quality vocoders by using re-synthesized speech, Acoust. Sci. & Tech., vol. 39, no. 3, pp. 263-265, May 2018. https://www.jstage.jst.go.jp/article/ast/39/3/39_E1779/_article/-char/en
