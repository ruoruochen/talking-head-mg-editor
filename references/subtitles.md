# Subtitle Defaults

Use this reference when a Chinese talking-head video has no visible subtitles/captions.

## Default Caption Style

Match the readable phone-first style from the user's current video:

- Language: Chinese original captions.
- Position: lower center, safely above the bottom edge.
- Font size: large mobile-readable, roughly equivalent to 58-72 px on a 1080x1920 canvas.
- Weight: bold or heavy.
- Text color: white.
- Stroke/shadow: thick black outline or shadow for contrast.
- Lines: 1-2 short lines per caption page.
- Density: avoid long subtitle blocks that compete with MG overlays.

## Placement With MG

Treat subtitles as protected screen real estate:

- Keep MG overlays out of the lower subtitle band.
- Prefer top, upper-left, upper-right, or upper-middle placements for outline nodes.
- If a speaker's face fills the upper area, use side-safe zones or shorten the MG duration.
- After enabling captions, render representative frames before claiming the layout is done.

## Workflow

1. Confirm whether subtitles are already burned into the video or enabled in ChatCut.
2. If no subtitles are visible, use ChatCut caption tools to enable Chinese captions from the transcript.
3. Style captions with large white bold text and black outline/shadow.
4. Verify captions on frames where MG overlays also appear.
5. Only then place or adjust MG nodes.
