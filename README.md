# MKV-Surround-To-Stero-FLAC
Converts MKV surround sound to Stereo in FLAC format. Highest Quality possible.

Run the command in the same directory where the MKV is.
- Does not require to rename the MKV
- Duplicates the MKV with a new Stereo FLAC track. **Does not delete the surround track in the output file!**
- Runs multi-threaded so should be pretty fast. Recommended to convert on an SSD so will be faster.

On my hard drive takes about 30 minutes for a 60GB file.
On the SSD can take up to 5 minutes max for a 60GB file.

---

**Multiple Channel Surround Sound To Stero**
**FLAC Multi Threaded**

``` bat
for /r %%i in (*.mkv) do (
    @ffmpeg.exe -hide_banner -v 32 -stats -y -i "%%i" -map 0:v -map 0:a:0 -map 0:a -map 0:s? -c:v copy -c:a:0 flac -threads 0 -filter:a:0 "pan=stereo|c0=c0+0.707*c2+0.707*c4|c1=c1+0.707*c2+0.707*c5" -c:a:1 copy -c:s copy -f matroska "%%~dpni [Stereo].mkv"
)
```

**Multiple Channel Surround Sound To Stero**
**FLAC Multi Threaded**
**Second Track**

```bat
for /r %%i in (*.mkv) do (
    @ffmpeg.exe -hide_banner -v 32 -stats -y -i "%%i" -map 0:v -map 0:a -map 0:s? -c:v copy -c:a copy -c:a:1 flac -threads 0 -filter:a:1 "pan=stereo|c0=c0+0.707*c2+0.707*c4|c1=c1+0.707*c2+0.707*c5" -c:s copy -f matroska "%%~dpni [Stereo].mkv"
)
```
