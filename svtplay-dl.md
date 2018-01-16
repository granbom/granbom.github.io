---
layout: page
permalink: /teknik/svtplay-dl/
title: svtplay-dl
description: En sida om svtplay-dl
---

Ett program för att ladda ner videofiler från olika playtjänster. Läs mer om det här: [https://svtplay-dl.se/](svtplay-dl.se)

## Installera från source

```shell

git clone https://github.com/spaam/svtplay-dl.git
make
sudo make install

```

## Parametrar

Nedan är ett urval av de parametrar som man vanligen använder.

### -A eller --all-episodes

Ladda ner alla filer i en serie

```shell

svtplay-dl -A https://play.se/url.till.ett.avsnitt

```

### -S eller --subtitle

Ladda ner undertextfil om det finns någon.

```shell

svtplay-dl -S https://play.se/url.till.ett.avsnitt

```

### --exclude

Ladda inte ner filer som innehåller något av orden i den kommaseparerade listan

```shell

svtplay-dl --exclude=syntolkat,teckentolkat https://play.se/url.till.ett.avsnitt

```

### --all-last

Ladda bara ner de senaste x episoderna. **Måste användas med -A**.

```shell

svtplay-dl -A --all-last=5 https://play.se/url.till.ett.avsnitt

```

### Kombinera det vanligaste

```shell

svtplay-dl -S -A --exclude=syntolkat,teckentolkat https://play.se/url.till.ett.avsnitt

```

## Konvertera

Konvertera alla *.ts filer i en katalog till .mkv och lägg till undertexter (.srt) till mkv. Kopiera bara streamarna (behåll alltså kvalitén) och sätt språk på ljud samt undertexterna. Ställer man in språket på ljudfiler och undertexter så kan exempelvis VLC välja de preferenser man har personligen, om man ställt in detta i VLC.

<div class="alert alert-info" role="alert">
<a href="../ffmpeg/" class="alert-link">ffmpeg</a> måste vara installerat på din dator.
</div>

### Linux och macOS

```bash

for file in *.ts; do ffmpeg -i "$file" -i "${file%.ts}".srt -metadata:s:a:0 language=eng -metadata:s:s:0 language=swe -c copy "${file%.ts}".mkv; done

```

### Windows
Skapa en .cmd fil med följande innehåll och kör den i samma katalog som filerna ligger i.

```bash

for %%f in (*.ts) do call ffmpeg -i "%%~f" -i "%%~nf.srt" -metadata:s:a:0 language=eng -metadata:s:s:0 language=swe -c copy "%%~nf.mkv"

```

## Förklaringar

### -metadata:s:a:0

* s=stream (ström)
* a=audio (ljud)
* 0=första streamen

denna sätter man alltså till language=eng (eller swe eller vilket språk nu ljudet är i)

### -metadata:s:s:0

* s=stream (ström)
* s=subtitle (undertext)
* 0=första streamen

denna sätter man alltså till language=swe (eller eng eller vilket språk nu undertexterna är på)

### -c copy

Att streamarna bara ska kopieras från en behållare (container, alltså filformatet) till en annan, strömmen i sig blir orörd. Behållarna i detta fallet är .ts (Transport Stream, vanligtvis video i h264 och ljud i aac) och .srt (SubRip undertextfil) till .mkv (Matroska)
Den andra strömmen är .srt (undertexterna), man lägger ihop video och audio strömmarna från .ts filen med undertext strömmen från .srt filen i en ny behållare som i detta fallet är .mkv (eftersom denna behållare/filformat, klarar av dessa tre typer av strömmar.
mp4 formatet klarar mig vetligen inte av .srt formatet av undertexter, vilket .mkv gör.

## Filformat

Alla ljud eller videofiler innehåller en eller flera strömmar (streams) alltså något strömmande data som i de vanligaste fallen är bild och ljud.
En mp3 fil innehåller exempelvis en ström av ljud, men själva mp3 filen är en *hållare* för strömmen.
En mp4 fil innehåller vanligtvis en video ström och en audio ström. Olika filformat klarar av olika många typer av strömmar, men de flesta klarar av massor med koprimeringstyper.
Olika filformat klarar av olika många strömmar och typer av strömmar.

### .ts (Transport Stream)

Innehåller vanligtvis en videostream kodad i h264 och en ljudstream kodad i aac.

### .mp4

Innehåller vanligtvis en videostream kodad i h264 och en ljudstream kodad i aac.

### .srt (SubRip)

Undertexter till en video i textformat, går att öppna i ett vanligt textprogram.
