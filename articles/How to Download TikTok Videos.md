# How to Download TikTok Videos

TikTok stores videos on short-lived CDN links — those long URLs with v16-webapp-prime.us.tiktok.com and ?expire= tokens.

Those links expire quickly and won’t work by themselves. 

The easiest way is to use the video page URL, which yt-dlp can automatically resolve into the proper stream.


## 1. Copy the TikTok Video URL

Open the video in your browser and copy the main video page link — not the direct .mp4.

- Example: https://www.tiktok.com/@dvnschmchr/video/7473513210667339054



## 2. Download with yt-dlp

Run this simple command:

```bash
yt-dlp "https://www.tiktok.com/@dvnschmchr/video/7473513210667339054"
```

That’s it — yt-dlp handles redirects, cookies, and merges the audio/video tracks automatically.


## 3. If You Get “403 Forbidden”

TikTok sometimes restricts downloads to sessions with valid cookies or headers.
You can fix that by letting yt-dlp use your browser cookies:

```bash
yt-dlp \
  --cookies-from-browser chrome \
  --add-header "Referer: https://www.tiktok.com/" \
  --user-agent "Mozilla/5.0 (Windows NT 10.0; Win64; x64)" \
  --merge-output-format mp4 \
  -o "%(title)s.%(ext)s" \
  "https://www.tiktok.com/@dvnschmchr/video/7473513210667339054"
```

Replace chrome with safari or firefox depending on your browser.


## 4. Downloading from Direct CDN Links

If you’ve already copied a URL that ends in .mp4?expire=..., you can use ffmpeg directly — just include the same headers:

```bash
ffmpeg \
  -headers "User-Agent: Mozilla/5.0\r\nReferer: https://www.tiktok.com/\r\n" \
  -i "https://v16-webapp-prime.us.tiktok.com/video/tos/.../file.mp4?expire=..." \
  -c copy tiktok_video.mp4
```

These links expire fast, so you’ll need a new one if it stops working.


## 5. Pro Tips

- `-N 8` → parallel downloads, faster for long videos.
- `--postprocessor-args "ffmpeg:-movflags +faststart"` → makes the MP4 instantly seekable.
- `-o "%(title)s.%(ext)s"` → names files after the TikTok title automatically.
- `yt-dlp -F URL` → lists all formats/resolutions before downloading.


## ✅ Want the Easy Way?

If you don’t want to touch the command line, try the web version instead:

👉 [TikTok Video Downloader](http://serp.ly/tiktok-video-downloader) — paste any TikTok link, download instantly (no watermark, no setup).

It uses the same backend logic (yt-dlp + ffmpeg) — just wrapped in a clean, fast web interface.