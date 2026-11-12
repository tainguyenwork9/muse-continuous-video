# Persistent project state

Use a dedicated project directory in Muse's actual persistent workspace. Determine the location from the current environment; do not assume a Codex or user-machine path. Use a unique project name and keep existing projects intact.

Maintain a readable project-state file, using Markdown or JSON according to available tools. Save it after each generation, repair, user decision, or export. It must contain enough information to resume without relying on chat memory:

- Original script and approved revision, exact dialogue, and script-to-clip mapping.
- Target duration, aspect ratio, style, voice descriptions, and output settings.
- Review stages enabled or explicitly waived; batch size, normally three.
- Continuity bible, approved references, and scripted state changes.
- Each clip's ID, source paths, version, actual duration, prompt, input references, returned snapshot IDs, boundary-frame timestamp, and dependency on previous clips.
- Inspection evidence, unavailable checks, unresolved defects, and repair-attempt counts.
- User approvals with the precise version approved; distinguish generated, inspected, awaiting review, approved, superseded, and stale states.
- Assembly order, trims, timeline offsets, audio choices, subtitle status, export paths, and delivery status.
- The next action and any pending user decision or per-message generation limit.

Store assets with stable, versioned filenames and save exact returned identifiers rather than reconstructing them. State files should reference local assets; do not include credentials, access tokens, or unnecessary account data. Keep runtime assets and private scripts outside the public skill repository.

On resume, read state, confirm referenced files exist, check available tools and whether saved snapshot context remains usable, and continue from the first incomplete step. An expired snapshot does not invalidate a good saved clip; use available approved frames/references and disclose any resulting limitation. Do not regenerate approved work solely because the chat is new.
