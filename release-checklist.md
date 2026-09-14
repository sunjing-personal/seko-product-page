# Seko release evidence

Record each state independently:

1. **Generated** — the Seko/Seedance source exists and the generation request is recorded.
2. **Mastered** — a browser-targeted output exists with source/output hashes.
3. **Media QA passed** — decode, cadence, PTS, and visual checks passed.
4. **Template wired** — the shared page source references the approved asset and poster.
5. **Local/LAN preview verified** — the target routes and viewport checks passed locally.
6. **Committed** — the intended branch contains the source and built-output changes.
7. **Remote pushed** — the exact remote and commit are recorded.
8. **Environment verified** — the deployed test/production route was opened and checked separately.

Do not report “published” or “live” when only steps 1–5 are complete. Keep a rollback asset/source snapshot until the environment check is complete.
