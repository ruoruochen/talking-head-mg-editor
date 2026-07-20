# Iteration Record

## 2026-07-20

### Initial Skill

Created `talking-head-mg-editor` for Chinese talking-head video editing in ChatCut.

Capabilities added:

- Add transcript-synced outline nodes.
- Add section titles and keyword pop-ups.
- Add comparison callouts with `✅` / `❌`.
- Align MG timing to actual spoken words instead of fixed animation timing.
- Avoid covering existing subtitles, face, mouth, and important gestures.
- Add captions first when a video has no subtitles.

### Cover As First Frame

Added cover image workflow.

Capabilities added:

- Ask for video series and episode number before cover design.
- Support cover image creation or use an existing cover image.
- Place cover image as the first frame/opening still in ChatCut.
- Preserve downstream subtitle/MG timing when inserting a cover at the beginning.
- For the `表达力觉醒` series, require the fixed top label: `🔥表达力觉醒 第x期`.

### Chinese Documentation

Added human-readable Chinese documentation.

Capabilities added:

- Keep `SKILL.md` in English for model execution stability.
- Add `README.zh-CN.md` so the user can understand the skill in Chinese.
