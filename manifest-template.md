# Seko run manifest template

Copy this into a versioned run directory and fill it with non-secret values.

```yaml
run_id: YYYYMMDD-short-name-vN
page_route: /cn/products/seko/
locales: [zh-CN, zh-TW, en]
generation:
  tool: Seko / Seedance
  model: REPLACE
  created_at: ISO-8601
  prompt_file: prompt.md
  reference_id: approved-reference-name
  private_source_url: OMIT_FROM_PUBLIC_REPO
  source_sha256: REPLACE
  source_media: {width: REPLACE, height: REPLACE, fps: REPLACE, frames: REPLACE, duration_s: REPLACE}
output:
  strategy: native-web-master | fixed-1920x400
  file: REPLACE
  sha256: REPLACE
  media: {codec: h264, pixel_format: yuv420p, width: REPLACE, height: REPLACE, fps: REPLACE, frames: REPLACE, duration_s: REPLACE}
  crop: null
qa:
  technical: pass | fail
  visual: pass | fail
  page_routes: pass | fail
  reviewer: REPLACE
  notes: REPLACE
release:
  asset_copied: true | false
  template_wired: true | false
  local_preview: true | false
  remote_pushed: true | false
  environment_verified: true | false
```
