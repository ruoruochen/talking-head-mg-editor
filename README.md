# talking-head-mg-editor

`talking-head-mg-editor` is a Codex skill for editing Chinese talking-head / 口播 videos in ChatCut. It adds transcript-synced outline nodes, section titles, keyword pop-ups, comparison callouts, MG animations, and captions when the source video does not already have subtitles.

## When To Use

Use this skill when you want Codex to:

- analyze a recorded Chinese口播 video;
- add大纲节点, 标题节点, or MG动画 in ChatCut;
- make keywords pop up exactly when they are spoken;
- avoid covering existing subtitles, the speaker's face, mouth, or important gestures;
- add Chinese subtitles first when the video has no captions.

## What It Does

The skill guides Codex to:

1. Inspect the ChatCut project and transcript.
2. Search the transcript for each spoken concept or list item.
3. Place every keyword/title node at the actual spoken frame.
4. Keep cumulative method nodes visible until the relevant section is finished.
5. Add captions first if subtitles are missing.
6. Verify the edited timeline with rendered frames before reporting completion.

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
