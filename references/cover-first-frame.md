# Cover Image As First Frame

Use this reference when the user asks to make a cover image, update a cover, or use the cover as the first frame/opening still of a talking-head video.

## Cover Design

Default format:

- Canvas: 1080x1920 vertical.
- Purpose: readable mobile cover, not a decorative poster.
- Before designing, ask the user to choose the video series and episode number.
- For the existing `表达力觉醒` series, the top series label is fixed as `🔥表达力觉醒 第x期`. Do not change it to other separators or variants such as `表达力觉醒｜第x期`.
- Main text: short, high-contrast, and close to the user's chosen title/cover wording.
- Visual priority: the speaker/person/product should be obvious in the first viewport when available.
- Style: match the video's MG language unless the user gives another reference. For the current user, prefer casual Xiaohongshu-style large text, black outline/shadow, and strong readable color.
- Avoid: tiny text, crowded paragraphs, formal slide style, generic gradient-only backgrounds, and text covering the face.

When the user already has a cover image, use it instead of generating a new cover unless they ask for redesign.

## Series Label

Always separate the cover into a reusable series label and a per-video cover title.

For `表达力觉醒`:

- Top label text: `🔥表达力觉醒 第x期`
- Replace `x` with the episode number provided by the user.
- Keep the label visually consistent across all videos in the series.
- Do not rewrite the series label based on the post title.

The bottom title is the click-oriented cover title. It can be shorter and punchier than the post title, and should use the strongest wording for the video's promise.

## Ways To Produce The Cover

Choose the least destructive option:

1. Existing cover file from the user:
   - Import it into ChatCut as an image asset.
   - Place it at the very beginning as a still image.

2. Frame-based cover:
   - Extract or inspect a flattering source frame.
   - Add title/cover text as editable MG or create a flattened raster cover if the user wants a finished image.

3. Generated cover:
   - Use image generation only when the user wants a new designed cover or no usable source frame exists.
   - Keep the generated image faithful to the video topic and avoid changing the speaker's identity.

## Timeline Placement

The cover must appear as the first visible frame when requested.

Default placement:

- Add the cover image at timeline frame 0.
- Duration: 30-60 frames (1-2 seconds at 30fps), unless the user asks for a longer title card.
- Original video begins immediately after the cover.

Alignment warning:

- Inserting a cover at frame 0 shifts the original A-roll later.
- If existing captions/MG nodes are already synced to the original timeline, use ripple/sequence-aware timeline edits so all dependent layers move together.
- If ripple cannot safely preserve sync, re-read the timeline and rebuild/adjust MG/caption timings after insertion.
- Do not place a cover on an upper track over the first video frames while leaving original audio underneath unless the user wants audio to start under the cover.

## Verification

After placement:

- Render frame 0 and confirm the cover is visible.
- Render the first frame after the cover ends and confirm the A-roll starts correctly.
- Spot-check at least one later MG/caption node to confirm timing was not shifted out of sync.
