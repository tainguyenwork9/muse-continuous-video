---
name: muse-continuous-video
description: Create a complete downloadable video and separate SRT subtitles from a detailed script using Muse Video. Use for videos longer than one approximately ten-second clip, including one-minute and longer projects, requiring consistent characters, environments, action, dialogue, and sound. Run end to end with automatic quality checks and resumable progress, without routine review pauses.
---

# Continuous Video Production for Muse

Turn the user's detailed script into a coherent finished MP4 and a separate SRT file. Work across genres and visual styles. Communicate in the user's language; preserve the script's language, names, meaning, and exact dialogue.

## Establish the project

Read the supplied script and existing project state first. Ask only for missing decisions: target duration, aspect ratio, visual style, and desired voice characteristics expressed in the prompt. Prioritize telling the complete script; a few seconds of duration variation are acceptable. If the script substantially exceeds the target, ask which constraint to change. Never silently rewrite, omit, reorder, or shorten meaningful content or dialogue.

Default to end-to-end automatic production: plan, establish references, storyboard internally as useful, generate sequentially, inspect and repair, assemble, subtitle, verify, and deliver. Do not ask the user to approve the plan, designs, storyboard, or every three clips. Make routine creative and editing choices within the script and user preferences, and continue after saving checkpoints. Enable review gates only when the user explicitly requests them. Preserve existing approvals, but do not invent user approval for automatically selected work.

Pause only for a required missing decision that cannot reasonably be inferred, a material script change, a tool refusal or unavailable required capability, an unresolved defect after the repair limit, or a verified tool/message limit. Give concise progress updates without turning them into approval requests. Lack of playback/listening alone is not a reason to stop production: disclose unverified aspects with the completed export.

Read [references/production.md](references/production.md) for the generation, continuity, editing, and verification procedure. Read [references/project-state.md](references/project-state.md) when creating or resuming project state.

## Actual capabilities, not assumed capabilities

The following baseline comes from the user's report of Muse documentation and prior use, not independent tests of the current session. Inspect the actual available tool schema and relevant installed tool instructions before calling anything. If they differ, record the discrepancy and adapt the plan.

- Muse Video is accessed through `media.generate_video`. Reported output is approximately ten seconds per clip, with no selectable duration, and at most six clips per message. Automatic production does not override actual limits; retries also count where applicable. Check current tool instructions. If a message limit is reached, save progress and request only the continuation message needed to resume, not scene approval. Never pretend to start a new user message or evade the limit.
- Image inputs and snapshot context can help preserve appearance. Reported identifiers include `snapshot_id` and `resume_from_snapshot_id`; use them only in the form supported by the current schema. They are not a guaranteed character lock.
- A frame from the preceding clip can guide the next clip's opening, but image conditioning is not guaranteed to reproduce that frame exactly. There is no verified end-frame control or true in-place video extension. Each generation produces a separate file.
- Generated clips may contain synthesized audio. Audio-track presence does not establish correct speech, music, voice identity, or synchronization. Audio input, fixed voice selection, and lip synchronization are not established capabilities. Voice descriptions are requested qualities, not promises of an exact voice.
- The user reports successful MP4 assembly with local FFmpeg and an installed `ffmpeg-skill`. Check what is actually available. Use installed instructions if present; otherwise use available FFmpeg directly. Do not require an unavailable skill, invent commands from a repository, or claim a tool is installed without checking.

## Completion contract

The final delivery consists of the MP4 and separate SRT, with working download links through the available delivery mechanism. During production, show reference images, storyboards, batch previews, and review exports as needed. Retain intermediate assets and state internally for future revisions when persistent storage is available; otherwise provide the recovery checkpoint described in project-state.md. Do not substitute prompts or a storyboard for the finished video.

Require evidence for verification claims. If playback or listening is unavailable, continue all feasible production and deliver the completed export with a concise list of aspects for the user to check. Never label speech, voice consistency, lip synchronization, or temporal smoothness as verified from still frames, metadata, or a successful export. Distinguish completed production from verified quality and user approval. If the user explicitly requested final approval, identify the file as a review export until that approval is given.

If a required capability is unavailable, save completed work and explain the concrete blocker and available next action. Do not claim a finished video exists when generation, assembly, or delivery failed.
