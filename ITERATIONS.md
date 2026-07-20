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

### Geometry, Node References, And Cover Removal

Updated the skill after user review of an `表达力觉醒` edit.

Changes made:

- Removed cover image generation and cover-as-first-frame behavior from this skill.
- Added a rule that standalone cover images must be handled outside this talking-head editing workflow unless the user explicitly asks for a video intro card.
- Added geometry verification before MG work so vertical 9:16 talking-head footage is not distorted by stale horizontal crop/scale values.
- Stored approved visual references in `assets/title-node-reference.png` and `assets/list-term-reference.png`.
- Required Codex to visually inspect those assets before making title nodes or list/term nodes.
- Fixed title node guidance to use the pink upper-left style with white outline and black shadow.
- Fixed list/term guidance to use the yellow black-stroke two-column style without cards or panels.
- Added the maintenance rule that future skill changes must update `SKILL.md`, `README.md`, `README.zh-CN.md`, and `ITERATIONS.md` together before publishing.
