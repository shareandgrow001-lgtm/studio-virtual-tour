# Studio WebGL Viewer v1.7 — Eased Tracking

Based on v1.5 (the reliable v1.2 four-frame GPU blending with nearest-cached frame skipping). The experimental optical-flow shader is removed.

## Changes
- **Eased cursor tracking**: the camera follows the cursor with exponential smoothing plus a maximum normalized movement speed. Sudden corner-to-corner jumps travel through intermediate camera positions over time.
- **Tracking slider (1–10)**: lower = more cinematic delay; higher = faster response. Default 5.
- **Predictive texture prefetch**: loads upcoming frames along the current camera travel direction.
- **No hold-last-complete-quartet**: each requested corner uses its nearest cached GPU texture until the correct image arrives.
- Preserves dynamic rows/columns, serpentine frame mapping, texture orientation fix, and GPU cache.

## Run
Run `python -m http.server 8000` in this folder, open http://localhost:8000, enter your grid dimensions and select the correct number of sequentially numbered Blender renders.

## Notes
- Cursor lag is intentional; use Tracking 7–9 if it feels too slow.
- Missing images can still cause temporary visual jumps; a slow connection or very large grid can overwhelm prefetch.
- Blending ghosting remains because the original bilinear interpolation is preserved.
- Test on the actual browser/GPU with your renders; syntax validation does not guarantee GPU performance.
