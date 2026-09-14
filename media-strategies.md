# Seko media output strategies

## Preferred: native web master

Use when the page can present the hero in a responsive 21:9 container.

- Preserve the source display ratio, frame count, PTS, and playback speed.
- Remux to fast-start if already H.264/yuv420p and browser-compatible.
- Otherwise encode H.264, yuv420p, 8-bit, with native dimensions or an exact-ratio lightweight size such as 2520×1080.
- Do not crop, pad, stretch, interpolate, or time-scale.

## Explicit fixed banner: 1920×400

Use only when the page contract requires this exact canvas.

- Use a uniform aspect-fill crop, not a non-uniform resize.
- Record source dimensions, crop window, horizontal anchor, vertical anchor, and output dimensions in the manifest.
- Preserve native FPS, duration, frame count, and PTS.
- Do not add black bars, interpolate frames, blur-fill edges, or change speed.

These are separate deliverables. Do not silently convert a native web master into a fixed banner or call a crop-free output “cropped”.
