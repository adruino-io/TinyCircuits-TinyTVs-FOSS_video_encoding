# TinyCircuits - TinyTVs - FOSS video encoding

This repository contains the ffmpeg prompts to create JPEG AVI files for playback on the following TinyCircuits platforms:
* TinyTV 2
* TinyTV Mini
* TinyTV DIY

Currently TinyCircuits only provides a video conversion tool for MacOS as well as Windows https://jmtinycircuits.github.io/TinyTV-Converter-App/

## Video conversion using ffmpeg

The following settings can be used to convert videos using ffmpeg https://ffmpeg.org/

This allows usage across most platforms.

### for TinyTV DIY Kit
- **with audio:** `ffmpeg -i input -c:a pcm_u8 -ar 10000 -af "pan=mono|FC=FR" -q:v 4 -c:v mjpeg -vf "scale=w=96:h=64:force_original_aspect_ratio=2,crop=96:64" -r 24 output.avi`
- **no audio:** `ffmpeg -i input -an -q:v 4 -c:v mjpeg -vf "scale=w=96:h=64:force_original_aspect_ratio=2,crop=96:64" -r 24 output.avi`

### for TinyTV 2:
- **with audio:** `ffmpeg -i input -c:a pcm_u8 -ar 10000 -af "pan=mono|FC=FR" -q:v 4 -c:v mjpeg -vf "scale=w=210:h=135:force_original_aspect_ratio=2,crop=210:135" -r 24 output.avi`
- **with louder audio:** `ffmpeg -i input -c:a pcm_u8 -ar 10000 -af "pan=mono|FC=FR,volume=4" -q:v 4 -c:v mjpeg -vf "scale=w=210:h=135:force_original_aspect_ratio=2,crop=210:135" -r 24 output.avi`
- **no audio:** `ffmpeg -i input -an -q:v 4 -c:v mjpeg -vf "scale=w=210:h=135:force_original_aspect_ratio=2,crop=210:135" -r 24 output.avi`

### for TinyTV Mini:
- **with audio:** `ffmpeg -i input -c:a pcm_u8 -ar 10000 -af "pan=mono|FC=FR" -q:v 4 -c:v mjpeg -vf "scale=w=64:h=64:force_original_aspect_ratio=2,crop=64:64" -r 24 output.avi`
- **no audio:** `ffmpeg -i input -an -q:v 4 -c:v mjpeg -vf "scale=w=64:h=64:force_original_aspect_ratio=2,crop=64:64" -r 24 output.avi`

## Adjustments:
- setting the string `"-q:v 0"` will result in little to no compression artifacts, but large files
- removing the string `"-q:v 4"` will result in strong compression, thus tiny files
- adding the string `"volume=..."` after `"pan=mono|FC=FR"` (e.g. `"pan=mono|FC=FR,volume=4"` icreases volume by factor four) can be used to adjust the audio volume

## Future fixes:
- due to lacking the respective hardware the settings for DIY kit and Mini could not be tested
- the strings can be optimized to reduce prompts
- the resulting video for TinyTV 2 is 216x134 px rather than 216x135 px (this did not result in any playback issues so far)
