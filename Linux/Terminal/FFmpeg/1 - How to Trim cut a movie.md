---
title: 1 - How to Trim cut a movie
tags:
  - Linux
  - FFmpeg
  - Cut
---

### 💬 Trim a video
🔰 Terminal

```shell
ffmpeg -i Narcos_S01E09.mkv -ss 00:39:50 -to 00:41:20 -c:v copy -c:a copy trimmedVideo.mkv
```
