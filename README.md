# talking-head-mg-editor

`talking-head-mg-editor` is a Codex skill for editing Chinese talking-head / 口播 videos in ChatCut. It adds transcript-synced outline nodes, section titles, keyword pop-ups, comparison callouts, MG animations, captions when the source video does not already have subtitles, and cover images that can be used as the first frame.

中文说明见 [README.zh-CN.md](README.zh-CN.md). Iteration history is tracked in [ITERATIONS.md](ITERATIONS.md).

## When To Use

Use this skill when you want Codex to:

- analyze a recorded Chinese口播 video;
- add大纲节点, 标题节点, or MG动画 in ChatCut;
- make keywords pop up exactly when they are spoken;
- avoid covering existing subtitles, the speaker's face, mouth, or important gestures;
- add Chinese subtitles first when the video has no captions.
- design a cover image and place it as the first frame/opening still.

## What It Does

The skill guides Codex to:

1. Inspect the ChatCut project and transcript.
2. Search the transcript for each spoken concept or list item.
3. Place every keyword/title node at the actual spoken frame.
4. Keep cumulative method nodes visible until the relevant section is finished.
5. Add captions first if subtitles are missing.
6. Ask for the video series and episode number before cover design.
7. For the `表达力觉醒` series, keep the top cover label fixed as `🔥表达力觉醒 第x期`.
8. Verify the edited timeline with rendered frames before reporting completion.

## Usage

Install or keep this folder at:

```text
~/.codex/skills/talking-head-mg-editor
```

Example prompt:

```text
帮我分析这个口播视频，按说话内容添加大纲/标题节点和MG动画；如果没有字幕，先补字幕。
```

```text
帮我给这个口播视频做封面，系列是表达力觉醒，第12期，封面作为第一帧。
```

## Notes

- This skill expects ChatCut editing tools to be available.
- It produces an editable ChatCut project by default, not an exported MP4.
- Export should only happen when the user explicitly asks to render/download/finalize.
- The default visual language is casual Xiaohongshu-style: large yellow or pink text, black stroke/shadow, and phone-first readability.
- The main execution instructions are written in English for model reliability; Chinese documentation is included for human reading.
