---
Title: ffmpeg
Description: En sida om ffmpeg
Author: PG Granbom
---

## ffmpeg
---
En applikation för att konvertera strömmar av ljud/bild från olika filtyper.

### Installera från source

```bash
git clone https://git.ffmpeg.org/ffmpeg.git
./configure --enable-pthreads --enable-version3 --enable-avresample --enable-gpl --enable-libass --enable-libfdk-aac --enable-libfreetype --enable-libmp3lame --enable-libopus --enable-librtmp --enable-libvorbis --enable-libvpx --enable-libx264 --enable-libx265 --enable-libxvid --enable-opencl --enable-openssl --enable-nonfree
make
make install
```
Följande måste vara installerat innan kompileringen
```bash
sudo apt install autoconf automake build-essential cmake git libass-dev libfreetype6-dev libsdl2-dev libtheora-dev libtool libva-dev libvdpau-dev libvorbis-dev libxcb1-dev libxcb-shm0-dev libxcb-xfixes0-dev mercurial pkg-config texinfo wget zlib1g-dev
sudo apt install yasm libx264-dev libx265-dev libvpx-dev libfdk-aac-dev libmp3lame-dev libopus-dev librtmp-dev libxvidcore-dev ocl-icd-opencl-dev
```
<div class="alert alert-info" role="alert">
Om du vill snabba på kompileringen något och har en
flerkärning processor (vilket de flesta har numera) så skriv <code>export MAKEFLAGS="-j4"</code> innan du börjar kompilera.
</div>

### Konvertera
Konvertera alla *.ts filer i en katalog till .mkv och lägg till undertexter (.srt) till mkv. Kopiera bara streamarna (behåll alltså kvalitén) och sätt språk på ljudstream samt undertexterna.

#### Linux
```bash
for file in *.ts; do ffmpeg -i "$file" -i "${file%.ts}".srt -metadata:s:a:0 language=eng -metadata:s:s:0 language=swe -c copy "${file%.ts}".mkv; done
```

#### Windows
Skapa en .cmd fil med följande innehåll och kör den i samma katalog som filerna ligger i.
```bash
for %%f in (*.ts) do call ffmpeg -i "%%~f" -i "%%~nf.srt" -metadata:s:a:0 language=eng -metadata:s:s:0 language=swe -c copy "%%~nf.mkv"
```
