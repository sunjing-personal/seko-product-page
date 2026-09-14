# Seko video and page QA checklist

## Media integrity

- [ ] Source and output decode completely with no non-zero decoder exit.
- [ ] Codec and pixel format are browser-compatible (normally H.264/yuv420p, 8-bit).
- [ ] Dimensions and display aspect ratio match the selected strategy.
- [ ] Duration, frame count, FPS, and frame timestamps are preserved unless explicitly approved otherwise.
- [ ] PTS are monotonic; no unexplained cadence outlier or exact duplicate frame.
- [ ] MP4 metadata is fast-start (`moov` available before media payload where the tool supports it).
- [ ] SHA-256 values are recorded for source and output.

## Visual review

- [ ] Fixed film/window geometry remains stable.
- [ ] Motion follows the approved direction and action beats.
- [ ] The principal crossing/action reads as one continuous physical event.
- [ ] No flicker, black frame, repeated first frame, teleport, geometry jump, or material flicker.
- [ ] No clipping, floating, reverse-gravity, or frozen-layer artifact.
- [ ] First/middle/last frames are reviewed as images, not only through metadata.

## Page review

- [ ] Poster, source path, and cache token are correct.
- [ ] `muted`, `loop`, `playsinline`, and `preload` match the page policy.
- [ ] Carousel transition stops or replaces the previous video's playback state.
- [ ] Direct route, refresh, back/forward, and homepage entry work.
- [ ] Desktop and approximately 390px mobile layouts keep the intended safe area.
- [ ] Autoplay-blocked and media-load-failed states remain usable.
