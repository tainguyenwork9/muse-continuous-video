---
name: muse-continuous-video
description: Create a complete downloadable video and separate SRT subtitles from a detailed script using Muse Video. Use for multi-clip projects requiring consistent characters, environments, action, dialogue, and sound, with review batches and resumable progress.
---

# Continuous Video Production for Muse

Turn the user's detailed script into a coherent finished MP4 and a separate SRT file. Work across genres and visual styles. Communicate in the user's language; preserve the script's language, names, meaning, and exact dialogue.

## Establish the project

Read the supplied script and existing project state first. Ask only for missing decisions: target duration, aspect ratio, visual style, and desired voice characteristics expressed in the prompt. Prioritize telling the complete script; a few seconds of duration variation are acceptable. If the script substantially exceeds the target, ask which constraint to change. Never silently rewrite, omit, reorder, or shorten meaningful content or dialogue.

Offer these review stages: scene breakdown, reference designs, storyboard, and batches of approximately three clips. They are optional: honor explicit requests to skip stages, and retain any approvals already given. In the absence of instructions, propose this review plan with the breakdown and obtain the user's choice before production. Do not infer approval from silence. Once the review plan is agreed, continue through unblocked work without repeatedly asking for permission.

Read [references/production.md](references/production.md) for the generation, continuity, editing, and verification procedure. Read [references/project-state.md](references/project-state.md) when creating or resuming project state.

## Actual capabilities, not assumed capabilities

The following baseline comes from the user's report of Muse documentation and prior use, not independent tests of the current session. Inspect the actual available tool schema and relevant installed tool instructions before calling anything. If they differ, record the discrepancy and adapt the plan.

- Muse Video is accessed through `media.generate_video`. Reported output is approximately ten seconds per clip, with no selectable duration, and at most six clips per message. Three-clip review batches do not override this limit; retries also count where applicable. If the message limit is reached, save progress and request the next user message.
- Image inputs and snapshot context can help preserve appearance. Reported identifiers include `snapshot_id` and `resume_from_snapshot_id`; use them only in the form supported by the current schema. They are not a guaranteed character lock.
- A frame from the preceding clip can guide the next clip's opening, but image conditioning is not guaranteed to reproduce that frame exactly. There is no verified end-frame control or true in-place video extension. Each generation produces a separate file.
- Generated clips may contain synthesized audio. Audio-track presence does not establish correct speech, music, voice identity, or synchronization. Audio input, fixed voice selection, and lip synchronization are not established capabilities. Voice descriptions are requested qualities, not promises of an exact voice.
- The user reports successful MP4 assembly with local FFmpeg and an installed `ffmpeg-skill`. Check what is actually available. Use installed instructions if present; otherwise use available FFmpeg directly. Do not require an unavailable skill, invent commands from a repository, or claim a tool is installed without checking.

## Completion contract

Deliver only the final MP4 and separate SRT as user-facing artifacts, with working download links through the available delivery mechanism. Retain intermediate assets and state internally for future revisions. Do not substitute prompts or a storyboard for the finished video.

Require evidence for verification claims. If playback or listening is unavailable, disclose that limitation and obtain the user's audiovisual review at the agreed batch stage. Never label speech, voice consistency, lip synchronization, or temporal smoothness as verified from still frames, metadata, or a successful export. If final approval is pending, identify the file as a review export rather than declaring the project approved.

If a required capability is unavailable, save completed work and explain the concrete blocker and available next action. Do not claim a finished video exists when generation, assembly, or delivery failed.
