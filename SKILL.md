---
name: seko-product-page
description: Create or update SenseTime Seko product pages and their hero banners, including Seko/Seedance generation handoff, video mastering, media QA, shared-site integration, multilingual route checks, and release evidence.
---

# Seko Product Page

Use this skill when the request involves a Seko product page, Seko hero/banner video, Seko page visual refresh, carousel asset replacement, or release validation. It covers the full path from an approved creative brief to a page-ready asset and verified route. It does not grant permission to call an external generation service, publish a site, or push a repository; obtain those permissions at the point of the mutation.

## Operating contract

- Treat the source video, page integration, local/LAN preview, and online release as separate states. Report each state separately.
- Keep every run in a versioned directory with a source/output manifest and SHA-256 values. Never put API keys, Seko account tokens, private asset URLs, or temporary access URLs in this skill or a public repository.
- Prefer the native 21:9 web-master path. Do not default to a 1920×400 crop merely because an old page used that size. If a fixed 1920×400 deliverable is explicitly required, use the crop path in [media-strategies.md](references/media-strategies.md) and document the anchor and crop window.
- Do not modify generated HTML directly. Find the shared page/template/generator source, wire the asset there, rebuild, and inspect the built output.
- Do not call a visually unapproved generation result “final”. Stop before release when geometry continuity, encoded timeline, or page-route checks fail.

## Workflow

### 1. Scope and inputs

Record the page route, locales, existing hero slides, poster assets, target viewport(s), video policy (`muted`, `loop`, `playsinline`, `preload`), and the requested conversion goal. Locate the existing Seko page template and asset root before editing. Preserve a rollback copy of the current source and rendered page reference.

Read [media-strategies.md](references/media-strategies.md) before choosing a video output strategy. Read [prompt-template.md](references/prompt-template.md) before creating or handing off a Seko/Seedance generation request.

### 2. Art direction and reference lock

Lock the non-negotiable geometry before generation: film strip, sprocket holes, window, camera position, horizon, and safe areas. Define motion direction, material behavior, start/middle/end beats, and explicit negative constraints. Use the existing hero still or approved keyframe as the reference. Do not ask the model to redesign the page composition while asking it to animate the hero.

### 3. Seko/Seedance generation

For the historical Seko banner workflow, the working baseline was native 21:9, 4K, 15 seconds, 24 fps. Treat these as a starting point, not an unconditional requirement; use the product brief when it specifies different values. Submit only after checking the expected compute cost, account authorization, and output rights.

Save the generation request, reference identifiers, prompt version, model/tool name, generation timestamp, and returned source asset into the run manifest. Keep private service URLs out of public commits.

### 4. Iteration gates

Review each generation at first frame, motion onset, the principal crossing/action beat, the middle, and the last frame. Reject a version when it has any of the following:

- a new rectangular slab, alternate window, or changed film geometry;
- an external wave that never becomes part of the referenced scene;
- time jumps, repeated first frames, teleporting objects, flicker, or structural deformation;
- water clipping through the window, floating, reverse gravity, or a frozen horizontal layer;
- unsafe text/logo placement or a composition that cannot survive the target viewport.

Keep rejected versions and the reason in the manifest. Only use compositing as a controlled repair after a source generation is close; do not mask a broken base geometry with a complex effect stack.

### 5. Web mastering

For the preferred native path, preserve source frame count, frame timestamps, playback speed, and display ratio. Remux to fast-start when the source is already browser-compatible; otherwise encode a native-dimension H.264/yuv420p 8-bit master. A lightweight 2520×1080 variant is acceptable when bandwidth requires it, provided the ratio, frame cadence, and PTS remain stable and no crop/padding is introduced.

For an explicitly requested fixed 1920×400 asset, use a documented uniform aspect-fill crop with a named horizontal/vertical anchor. Never stretch, add black bars, interpolate frames, change frame rate, or time-scale the clip just to hit a size.

### 6. Technical and visual QA

Run the repository's media QA tool when available; otherwise reproduce the checks in [qa-checklist.md](references/qa-checklist.md). Technical checks must include complete decode, codec, pixel format, bit depth, dimensions, duration, frame count, monotonic PTS, cadence outliers, duplicate frames, and fast-start metadata. Visual checks must include fixed geometry, continuous motion, no flicker/black frames, and desktop plus 390px review.

Do not proceed on a non-zero decode result or unexplained cadence anomaly. Record the QA command, tool version, summary, and reviewer decision in the run manifest.

### 7. Page integration

Copy the approved, QA-passed asset into the page's versioned asset directory. Update the shared Seko page source so the hero video has the correct poster, `muted`, `loop`, `playsinline`, and `preload` behavior. Keep carousel state and video state synchronized when slides change. Update cache tokens only through the normal build source. Do not patch a generated page in `dist/` or an exported HTML snapshot.

### 8. Locale, responsive, and route QA

Build all affected locales and test the direct route, homepage entry, refresh, back/forward navigation, carousel transitions, and failed-video fallback. Check desktop, ordinary laptop width, and approximately 390px mobile width. Confirm that a previous slide does not continue playing after transition, that a poster does not flash unexpectedly, and that the hero remains usable when autoplay is blocked.

### 9. Release and handoff

Use [release-checklist.md](references/release-checklist.md) to distinguish:

1. source generated;
2. web master prepared;
3. media QA passed;
4. template wired;
5. local/LAN preview verified;
6. package committed;
7. remote pushed;
8. test/production deployment verified.

Never collapse these into “live”. If the user requests GitHub or SkillHub publication, verify the exact destination repository, authentication, and publication mechanism first; the skill itself does not assume any remote or token.

## Reusable artifacts

- [prompt-template.md](references/prompt-template.md): generation brief and negative constraints.
- [media-strategies.md](references/media-strategies.md): native web-master versus explicit fixed-banner crop.
- [qa-checklist.md](references/qa-checklist.md): technical and visual acceptance checks.
- [release-checklist.md](references/release-checklist.md): evidence-based integration and release states.
- [manifest-template.md](references/manifest-template.md): versioned run record without secrets.
