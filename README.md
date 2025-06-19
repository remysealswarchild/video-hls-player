
# 🎬 HLS Video Streaming with FFmpeg and GitHub Pages

This project showcases a complete pipeline for encoding a video into multiple resolutions using **FFmpeg**, segmenting it for HTTP Live Streaming (HLS), and deploying it to **GitHub Pages** where it can be streamed via browser using **hls.js**.

---

## 🎯 Project Objectives

- 🔄 Encode video into 360p, 480p, 720p, and 1080p resolutions
- 🧩 Segment videos into 2-second `.ts` chunks
- 📄 Generate variant and master `.m3u8` playlists
- 🚀 Deploy content to GitHub Pages
- 🎥 Stream via a modern browser using `hls.js`

---

## 🛠️ Technologies Used

- `FFmpeg` – video encoding and HLS packaging
- `Bash` – script automation
- `HLS.js` – JavaScript-based HLS player
- `GitHub Pages` – static site hosting
- *(Optional)* `GitHub Actions` – automated deployment

---

## 📁 Project Structure

```
video-hls-project/
├── scripts/
│   └── encode.sh              # FFmpeg automation script
│
├── web/                       # Public deployment folder
│   ├── index.html             # HLS.js video player
│   ├── master.m3u8            # HLS master playlist
│   ├── 360p/                  # Variant streams with segments
│   ├── 480p/
│   ├── 720p/
│   └── 1080p/
│
└── .github/workflows/
    └── deploy.yml             # Optional: GitHub Actions deployment
```

---

## ⚙️ How It Works

### 1. 🧪 Encode with FFmpeg

Run the encoding script:

```bash
chmod +x scripts/encode.sh
./scripts/encode.sh Sample.mp4
```

This creates:
- Multiple folders with `.ts` segments and `playlist.m3u8` for each resolution
- A `master.m3u8` linking them for adaptive playback

### 2. 🧾 Output Structure (per resolution)

```
playlist.m3u8
segment_000.ts
segment_001.ts
...
```

---

## 🌍 Deployment via GitHub Pages

### 🔁 Option 1: Manual Deployment

1. Push everything inside the `web/` folder to a GitHub repo.
2. Enable GitHub Pages in repo **Settings > Pages**.
3. Choose source: `main` branch and `/ (root)`.

✅ Your streaming player will be live at:

```
https://<your-username>.github.io/<repo-name>/
```

e.g.

```
https://remysealswarchild.github.io/video-hls-project/
```

---

## 🎬 HLS Player (index.html)

Your HTML5 page uses `hls.js` to stream the video from `master.m3u8`:

```html
<video id="video" width="640" height="360" controls></video>
<script src="https://cdn.jsdelivr.net/npm/hls.js@latest"></script>
<script>
  const video = document.getElementById('video');
  if (Hls.isSupported()) {
    const hls = new Hls();
    hls.loadSource('master.m3u8');
    hls.attachMedia(video);
    hls.on(Hls.Events.MANIFEST_PARSED, () => video.play());
  } else if (video.canPlayType('application/vnd.apple.mpegurl')) {
    video.src = 'master.m3u8';
    video.addEventListener('loadedmetadata', () => video.play());
  }
</script>
```

---

## 🧹 Recommended `.gitignore`

```gitignore
*.ts
*.mp4
scripts/
!web/index.html
!web/master.m3u8
!web/*/playlist.m3u8
```

---

## 🚧 Future Enhancements

- [ ] Add MPEG-DASH support
- [ ] Make the layout responsive for mobile
- [ ] Add buttons to manually switch resolutions
- [ ] Integrate subtitles and thumbnails
- [ ] Auto-generate metadata and previews

---

## 📄 License

Licensed under the MIT License. See [LICENSE](LICENSE) for details.

---

## 🙋 Author

**Derrick Tunde**  
🔗 [GitHub](https://github.com/remysealswarchild)
