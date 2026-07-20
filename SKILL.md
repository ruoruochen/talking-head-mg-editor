---
name: talking-head-mg-editor
description: Edit Chinese talking-head / 口播 videos in ChatCut by adding transcript-synced outline nodes, section titles, comparison callouts, keyword/list pop-ups, MG animations, and captions when missing. Use when the user asks to 剪辑口播视频, 加大纲节点, 加标题节点, 加动效/MG动画, 按说话内容弹出文字, 避开原字幕, or add subtitles before visual overlays.
---

# Talking Head MG Editor

## Purpose

Use this skill to turn a recorded Chinese talking-head video into an editable ChatCut timeline with clear outline/title Motion Graphics that follow the speaker's actual words. The default output is a previewable ChatCut project, not an exported MP4 unless the user asks for export.

Pair this skill with ChatCut skills as needed:

- `chatcut:chatcut-plugin-basics` for project targeting, import, timeline edits, and editor links.
- `chatcut:talking-head-guide` for speech-led editing judgment.
- `chatcut:create-motion-graphics` for hand-authored JSX Motion Graphics.
- `chatcut:transcription` when subtitles/captions are missing or need style changes.
- `chatcut:verification` before reporting visible edits.

## Maintenance Rule

When this skill changes, update `SKILL.md`, `README.md`, `README.zh-CN.md`, and `ITERATIONS.md` together before publishing. Do not leave the READMEs describing old behavior. If visual reference styles change, update the images in `assets/` and mention those assets in both READMEs.

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

3. Verify the A-roll video geometry before adding overlays.
   - Read the source asset dimensions and the timeline item geometry.
   - Never leave a vertical talking-head video with horizontal-import crop/scale values such as huge negative `left`, oversized `width`, or nonzero side crop when the source is actually 9:16.
   - If metadata changed after upload/transcription, re-read the asset and reset the main clip to non-distorted 9:16 placement before MG work. For a 1080x1920 timeline and 9:16 source, the normal full-frame placement is `left=0`, `top=0`, `width=1080`, `height=1920`, `crop*=0`.
   - If the source is truly horizontal, do not stretch it. Use `fit:"cover"` only when face and important content remain visible; otherwise use a deliberate contain/layout treatment and verify pixels.
   - Render an early frame before and after geometry fixes. Check face shape and background proportions, not just item metadata.

4. Build a node map before editing.
   - Chapter title nodes: section transitions, such as `1. 逻辑能力`.
   - Keyword nodes: concepts that should pop up as spoken.
   - Sequence nodes: methods/steps that should reveal line by line.
   - Contrast nodes: use `✅` / `❌` when the speech has positive/negative contrast.
   - Recap nodes: final review points, also revealed according to the recap speech timing.

5. Create a small set of reusable MG assets.
   - Use the fixed title style below for section headers and chapter transitions.
   - Use the fixed list/term style below for concept lists, nouns, named abilities, method steps, and recap points.
   - Before creating title or list/term MG assets, open and visually inspect the reference images in `assets/title-node-reference.png` and `assets/list-term-reference.png`. Do not rely on memory or the text description alone.
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
   - Check that the first frame starts with the actual edited video, not a generated cover/title-card, unless the user explicitly asked for an intro card in the video.
   - Check that text is readable, does not cover the face, does not cover subtitles, and appears only after the matching spoken content starts.

## Visual Style Defaults

For this user's current口播 style, default to these fixed visual references. These images are part of this skill and must be inspected when making matching MG assets:

- Section/title node style: open `assets/title-node-reference.png` and match it. The intended look is upper-left chunky pink title text, white outline, black/drop shadow, and smaller white italic/bold supporting lines underneath. Use this for chapter titles such as `1.亲情场景`, `2.友情场景`, `答案钓鱼法三步`. If the section includes a positive/negative contrast, show short supporting lines like `✅ 给选择` and `❌ 直接命令` under the pink title. Do not use generic rounded cards, gradient cards, or centered presentation blocks for title nodes.
- Concept/list/noun style: open `assets/list-term-reference.png` and match it. The intended look is bright yellow text, black stroke, no card background, arranged as two balanced columns near the lower-middle area above subtitles. Use this for 罗列观点、名词、能力词、步骤词、总结词, for example `逻辑思维能力 / 深度思考能力 / 概括能力 / 运用词汇能力`. Keep text short, bold, and phone-readable. Do not wrap these terms in cards, bubbles, panels, or decorative containers.
- Comparisons: `✅` for the recommended/positive expression and `❌` for the avoided/negative expression.
- Placement: title nodes usually upper-left; list/term nodes usually lower-middle but above the caption band. Avoid face, mouth, hands when important, and subtitles.
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

## Cover Handling

Do not generate a cover image in this skill and do not place a cover or title-card at the beginning of the edit by default.

If the user asks for a cover image, treat it as a separate task outside this talking-head editing skill unless they explicitly say it should be inserted into the video. A standalone cover image should be delivered as a separate image file, not mixed into the ChatCut timeline.

If a user explicitly asks for an intro card inside the video, make it clear that this is a video intro/title-card, not the standalone cover workflow, and then keep all captions and MG nodes synchronized after insertion.

## Handoff

After edits, provide the ChatCut editor URL for preview. Do not export unless the user explicitly asks to render/download/finalize the video.
