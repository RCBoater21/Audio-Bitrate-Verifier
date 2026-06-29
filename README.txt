AUDIO BITRATE VERIFIER 1.0
==========================

Portable 64-bit Windows application for measuring the average encoded bitrate
of audio files and comparing it with the bitrate reported by the file/codec.
No installation or administrator access is required.

QUICK START
-----------
1. Extract the entire ZIP to a normal writable folder.
2. Run AudioBitrateVerifier.exe.
3. On first use, the app may ask to download the portable FFprobe runtime
   (about 76 MB). It is stored in the local "runtime" folder.
4. Select an audio directory, choose whether to include subfolders, and press Run.

RESULT COLUMNS
--------------
Reported kbps
    The first audio stream's reported bit_rate value. If that is unavailable,
    the app checks explicit bitrate/BPS tags.

Measured kbps
    The sum of the compressed audio packet bytes, multiplied by 8 and divided
    by the stream duration. Artwork, tags, and container overhead are excluded.

Green text / MATCH
    Reported and measured values differ by no more than 3%, with a minimum
    tolerance of 2 kbps.

Red text / MISMATCH
    The reported value is outside that tolerance.

Neutral text / NO REPORTED BITRATE
    The encoded bitrate was measured, but the file did not expose a comparable
    reported bitrate. This is common with some lossless formats.

IMPORTANT INTERPRETATION NOTES
------------------------------
- A red result is not automatically evidence of a damaged or fake file. With
  VBR codecs, a nominal target bitrate can legitimately differ from the actual
  average, especially for unusually simple or complex audio.
- This app measures the encoded packet bitrate. It cannot determine whether a
  320 kbps file was transcoded from a lower-quality source, and it does not
  estimate spectral quality.
- Only the first audio stream in each file is analyzed.
- DRM-protected or corrupted files may show an error.
- Files are read only. The app never changes audio files.

FORMATS
-------
The scanner recognizes common MP3, FLAC, WAV, M4A/AAC/ALAC, OGG/Vorbis, Opus,
WMA, AIFF, APE, WavPack, TTA, AC-3/E-AC-3, DTS, AMR, MKA, WebM, MP4, CAF, AU,
DSF/DFF, TrueHD/MLP, Musepack, TAK, OptimFROG, VOC, Audible and related file
extensions. Actual decoding support comes from FFprobe.

FFPROBE RUNTIME
---------------
The application first checks for:
  - ffprobe.exe beside the application
  - runtime\ffprobe.exe
  - tools\ffprobe.exe
  - ffprobe.exe on PATH

If none is found, it offers to download the current BtbN FFmpeg Windows shared
build from GitHub and extracts only ffprobe.exe, its required DLLs, and license
files. The FFmpeg project and BtbN builds are separate third-party projects.

REBUILDING
----------
The source is included in the separate source package. Install Go 1.20 or newer,
then run source\build.bat. The application uses only the Go standard library and
native Windows controls.

BUILD INFORMATION
-----------------
Target: Windows x64 GUI
SHA-256 (AudioBitrateVerifier.exe):
7b9c82757bfdba6180c801cc97dd069a929f3a63ca00d2c582cb3bd87674384b
