# Video2X evaluation — 2026-09-18

Real test of [k4yt3x/video2x](https://github.com/k4yt3x/video2x) (21.7k stars,
AGPL-3.0) against a real clip of Rexx's own footage — his stairs shot, the
one used in the STAIRS → COFFEE → MEDICATION video opener.

## Setup

- **Binary**: `video2x-windows-amd64.zip`, release 6.4.0 (Jan 2025), CLI
  build — not redistributed here, download it fresh from the
  [official release page](https://github.com/k4yt3x/video2x/releases)
- **GPU**: NVIDIA RTX 2080 SUPER, auto-detected via Vulkan
- **Source clip**: `IMG_1072_browser_safe_720p.mp4` (720x1280, real phone
  footage, not a stock/test clip)

## Result: the model choice matters enormously

| Model | Scale | Verdict |
|---|---|---|
| `realesr-animevideov3` | 2x | Barely any improvement — this model is tuned for anime/cartoon content, not real footage |
| `realesrgan-plus` | 4x | **Real, visible improvement** — carpet fibers went from blurry mush to distinct threads. This is the general-purpose real-world photo model |

See `frames/` for the actual comparison images — `original.png` vs
`upscaled.png` (2x anime model) vs `plus4x-full.png` (4x real-world model,
the one that actually worked) vs the lanczos baseline for reference.

## Speed

~20 seconds to process 3 seconds of 30fps footage (90 frames) on the RTX
2080 SUPER at 2x. A full ~40s film would take roughly 4-5 minutes.

## Use case

Confirmed good fit for POV/walking footage and other real-camera content
with compression softness — not for content that's already clean (e.g.
Blender/CG renders).

## License note

AGPL-3.0. Fine to run as our own internal tool; the AGPL network-service
clause only bites if we turned this into a hosted service others call over
a network, which isn't the plan.
