# talking-head-mg-editor

`talking-head-mg-editor` is a Codex skill for editing Chinese talking-head / 口播 videos in ChatCut. It adds transcript-synced outline nodes, section titles, keyword/list pop-ups, comparison callouts, MG animations, and captions when the source video does not already have subtitles.

中文说明见 [README.zh-CN.md](README.zh-CN.md). Iteration history is tracked in [ITERATIONS.md](ITERATIONS.md).

## When To Use

Use this skill when you want Codex to:

- analyze a recorded Chinese口播 video;
- add大纲节点, 标题节点, or MG动画 in ChatCut;
- make keywords pop up exactly when they are spoken;
- avoid covering existing subtitles, the speaker's face, mouth, or important gestures;
- add Chinese subtitles first when the video has no captions;
- check and fix the main talking-head video geometry before adding overlays.

## What It Does

The skill guides Codex to:

1. Inspect the ChatCut project and transcript.
2. Search the transcript for each spoken concept or list item.
3. Place every keyword/title node at the actual spoken frame.
4. Keep cumulative method nodes visible until the relevant section is finished.
5. Verify that vertical 9:16 footage is not stretched or left with stale horizontal crop values.
6. Add captions first if subtitles are missing.
7. Use the stored title-node and list/term reference images before designing MG nodes.
8. Verify the edited timeline with rendered frames before reporting completion.

## Visual References

This skill stores the user's approved node references:

- `assets/title-node-reference.png`: title/chapter node style, with upper-left pink title text, white outline, black shadow, and short supporting lines.
- `assets/list-term-reference.png`: list/noun/term node style, with bold yellow text, black stroke, no card background, and a two-column lower-middle layout above subtitles.

Codex must inspect these images before making matching Motion Graphics. Text-only phrases like "use image 2 style" are not enough.

## Usage

Install or keep this folder at:

```text
~/.codex/skills/talking-head-mg-editor
```

Example prompt:

```text
帮我分析这个口播视频，按说话内容添加大纲/标题节点和MG动画；如果没有字幕，先补字幕。
```

## Notes

- This skill expects ChatCut editing tools to be available.
- It produces an editable ChatCut project by default, not an exported MP4.
- Export should only happen when the user explicitly asks to render/download/finalize.
- The default visual language is casual Xiaohongshu-style: large yellow or pink text, black stroke/shadow, and phone-first readability.
- Cover image generation is intentionally outside this skill. Do not create or insert a cover/title-card in the video unless the user explicitly asks for a video intro card.
- The main execution instructions are written in English for model reliability; Chinese documentation is included for human reading.
- Maintenance rule: every skill behavior update must also update `README.md`, `README.zh-CN.md`, and `ITERATIONS.md` before publishing.
