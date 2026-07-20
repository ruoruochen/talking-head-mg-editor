---
name: talking-head-mg-editor
description: Edit Chinese talking-head / 口播 videos in ChatCut by adding transcript-synced outline nodes, section titles, comparison callouts, keyword pop-ups, MG animations, captions when missing, and a cover image used as the first frame/opening still. Use when the user asks to 剪辑口播视频, 加大纲节点, 加标题节点, 加动效/MG动画, 按说话内容弹出文字, 避开原字幕, 制作封面图, 把封面作为第一帧, or add subtitles before visual overlays.
---

# Talking Head MG Editor

## Purpose

Use this skill to turn a recorded Chinese talking-head video into an editable ChatCut timeline with clear outline/title Motion Graphics that follow the speaker's actual words. It can also create a cover image and place it as the first frame/opening still. The default output is a previewable ChatCut project, not an exported MP4 unless the user asks for export.

Pair this skill with ChatCut skills as needed:

- `chatcut:chatcut-plugin-basics` for project targeting, import, timeline edits, and editor links.
- `chatcut:talking-head-guide` for speech-led editing judgment.
- `chatcut:create-motion-graphics` for hand-authored JSX Motion Graphics.
- `chatcut:transcription` when subtitles/captions are missing or need style changes.
- `imagegen` or ChatCut image-generation tools when a new raster cover image is needed.
- `chatcut:verification` before reporting visible edits.

## Core Rule

Synchronize visual nodes to the transcript, not to a fixed animation rhythm.

When the speaker lists concepts, do not show all concepts at once unless the speaker already finished the list. Use `find_transcript` with `includeWordTimestamps: true` to locate the exact frame where each concept is spoken, then place each keyword/item as its own timeline item so it pops in at that word and remains visible until the section/list ends.

Examples:

- For "逻辑能力、概括能力、深度思考能力，还有内容和词汇的积累能力", place four independent keyword items at the frames where each phrase starts.
- For "第一个 1，是结论先行。中间的 2，是给出两个支撑观点。最后一个 1，是重述结论", show `121原则` first, then reveal `1个结论先行`, `2个支撑观点`, and `1次重述结论` at their actual spoken frames. Hide the whole node only after the speaker finishes the last line.

## Workflow

1. Inspect the project and transcript.
   - Read the active timeline first.
   - Use transcript search for section phrases, list items, comparison terms, and recap words.
   - For timing-sensitive nodes, search each visible phrase separately with word timestamps.

2. Check subtitles before adding MG overlays.
   - If the video already has burned-in subtitles or ChatCut captions, keep all MG above or away from the subtitle band.
   - If the video has no subtitles, add ChatCut captions before final MG placement. Use the subtitle style described in [references/subtitles.md](references/subtitles.md).
   - After adding captions, verify the final MG positions again because captions define the bottom safe zone.

3. Decide whether a cover image is needed.
   - If the user asks for a cover or first-frame card, make the cover before final export/review.
   - Before cover design, ask for the video series and episode number. For the `表达力觉醒` series, the top label must be exactly `🔥表达力觉醒 第x期`.
   - If the user already made a cover, import/use that cover and place it at the start instead of generating a new one.
   - If the user has not specified title/cover copy, derive it from the video topic, transcript hook, or user's known title. Keep it short and mobile-readable.
   - See [references/cover-first-frame.md](references/cover-first-frame.md) for cover design and placement rules.

4. Build a node map before editing.
   - Chapter title nodes: section transitions, such as `1. 逻辑能力`.
   - Keyword nodes: concepts that should pop up as spoken.
   - Sequence nodes: methods/steps that should reveal line by line.
   - Contrast nodes: use `✅` / `❌` when the speech has positive/negative contrast.
   - Recap nodes: final review points, also revealed according to the recap speech timing.

5. Create a small set of reusable MG assets.
   - Use one title style for section headers.
   - Use one yellow black-stroke keyword style for concepts and list items.
   - Use one comparison style only when both sides should appear near each other. If contrast points are spoken far apart, split them into separate keyword items.
   - Do not create a new asset for every text variation when item-level property overrides can reuse the same visual role.

6. Place items by spoken frame.
   - Use `find_transcript` results as the source of timing truth.
   - Start each keyword item at the frame where the spoken phrase starts.
   - Let earlier revealed keywords remain until the list or method finishes when that helps the viewer see the structure.
   - End titles/method blocks after the speaker finishes the last relevant phrase, not after an arbitrary 3 seconds.
   - Use multiple video tracks for overlapping keyword items when they need to remain visible together.

7. Verify in ChatCut.
   - Re-read the timeline after edits.
   - Render representative frames with `view_timeline_frames`.
   - Inspect actual pixels when possible; do not rely only on successful tool responses.
   - Check that the first frame shows the cover when a cover was requested.
   - Check that text is readable, does not cover the face, does not cover subtitles, and appears only after the matching spoken content starts.

## Visual Style Defaults

For this user's current口播 style, default to:

- Section title: chunky pink text, black stroke/shadow, top-left or upper safe area.
- Concept/list item: bright yellow text, black stroke, strong pop-in, no card background.
- Comparisons: `✅` for the recommended/positive expression and `❌` for the avoided/negative expression.
- Placement: top or upper-middle safe area, avoiding face, mouth, hands when important, and subtitles.
- Tone: casual Xiaohongshu-style emphasis, not formal presentation slides.

Keep text large enough to read on a phone. Prefer fewer words per node. If a phrase is long, shorten it to the spoken concept rather than covering the frame.

## Timing Heuristics

- Chapter titles can appear at the section start and last about 2-4 seconds unless the speaker is explaining a named framework; then keep the framework title until its last sub-point finishes.
- A concept should pop in no earlier than the first frame of the spoken concept.
- A sequence item should remain visible until the sequence completes if cumulative structure matters.
- A contrast callout should appear when the contrasted idea is spoken. If `✅` and `❌` are discussed far apart, do not show them together from the first point.
- Recap nodes should follow the recap speech item by item.

## Subtitle Handling

If subtitles are absent, add captions before placing final MG overlays. See [references/subtitles.md](references/subtitles.md) for the default Chinese caption style and placement.

Never create normal timeline items for captions. Use ChatCut caption tools. Captions are a singleton overlay and should be styled/positioned through the caption workflow.

## Cover As First Frame

When the user requests a cover image or says the cover should become the first frame, read [references/cover-first-frame.md](references/cover-first-frame.md). The cover should be a real first-frame/opening still in the timeline, not only a separate design suggestion.

Default behavior:

- Create or use a 1080x1920 vertical cover.
- Use the video's strongest title/cover copy.
- Keep the speaker/product/person as the first-viewport signal when available.
- Place the cover at the beginning for about 1-2 seconds unless the user specifies a different duration.
- Keep the original video after the cover. If inserting the cover shifts the A-roll later, keep captions and MG nodes aligned by using ripple/sequence-aware timeline edits or by rebuilding node timings after insertion.
- Verify frame 0 after placement.

## Handoff

After edits, provide the ChatCut editor URL for preview. Do not export unless the user explicitly asks to render/download/finalize the video.
