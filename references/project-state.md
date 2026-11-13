# Persistent project state

Use a dedicated project directory in Muse's actual persistent workspace. Determine the location from the current environment; do not assume a Codex or user-machine path. Use a unique project name and keep existing projects intact.

If persistent storage is unavailable, post a compact recovery state block in chat at each checkpoint for the user to paste back on resume. Include approved decisions, available media links/identifiers, pending work, and verification gaps. Explain that the block preserves instructions, not media: temporary files, links, and snapshots may expire. If the user wants to retain intermediates, provide available downloads on request; do not promise those files will survive the session.

Maintain a readable project-state file, using Markdown or JSON according to available tools. Save it after each generation, repair, user decision, or export. It must contain enough information to resume without relying on chat memory:

- Original script and approved revision, exact dialogue, and script-to-clip mapping.
- Target duration, aspect ratio, style, voice descriptions, and output settings.
- Audio strategy, measured usable clip durations, estimated remaining clips, and current-message quota usage (including retries/refusals where counted).
- Execution mode, automatic by default; review stages and cadence only if explicitly requested. Checkpoints never imply a review pause.
- Continuity bible, approved references, and scripted state changes.
- Each clip's ID, source paths, version, actual duration, prompt, input references, returned snapshot IDs, boundary-frame timestamp, and dependency on previous clips.
- Inspection evidence, unavailable checks, unresolved defects, and repair-attempt counts.
- User approvals with the precise version approved; distinguish generated, inspected, selected_for_assembly, awaiting review, approved, superseded, and stale states. Automatic selection is not user approval; record unresolved verification gaps separately.
- Assembly order, trims, timeline offsets, audio choices, subtitle status, export paths, and delivery status.
- Per-join source versions, intended transition, motion state on each side, diagnosis/evidence, paired cut points with frame/time conventions, repair count, and rendered-join verification status.
- The next action and any pending user decision or per-message generation limit.

Store assets with stable, versioned filenames and save exact returned identifiers rather than reconstructing them. State files should reference local assets; do not include credentials, access tokens, or unnecessary account data. Keep runtime assets and private scripts outside the public skill repository.

Where supported, write updates to a temporary file in the same directory, validate that it parses, then atomically replace the state file. Preserve the last valid checkpoint if writing or validation fails. Otherwise use versioned checkpoints and explicitly identify the latest complete one.

Use this compact JSON shape as a starting point, extending it with the required detail above. Null means unknown, not verified; empty collections contain no recorded work. Keep revisions and paths explicit rather than assuming that the newest file is approved.

```json
{
  "schema_version": 1,
  "project_id": null,
  "script": {"path": null, "approved_revision": null, "beat_map": []},
  "settings": {"target_seconds": null, "aspect_ratio": null, "style": null, "voice": null},
  "review": {"mode": "automatic", "batch_size": null, "enabled_stages": [], "waived_stages": [], "approvals": []},
  "continuity": {"bible_path": null, "original_references": [], "scripted_changes": []},
  "audio": {"strategy": null, "assets": [], "target_lufs": null, "measured_lufs": null, "true_peak_dbtp": null},
  "budget": {"usable_seconds_measured": null, "remaining_clips_estimate": null, "message_limit": 6, "message_usage": 0},
  "clips": [],
  "timeline": [],
  "joins": [],
  "exports": {"mp4": null, "srt": null, "subtitle_status": "not_started", "delivery_status": "not_started"},
  "unverified_checks": [],
  "pending_decision": null,
  "next_action": null
}
```

For each clip record, include ID/version/status, script beats and exact lines, source path, prompt, references, snapshot IDs, dependency IDs/versions, boundary-frame path/timestamp, source duration, trim in/out, retained duration, repair count, refusals, inspection evidence, and approval for that version. Timeline entries reference those versions and final start/end offsets. Update message_usage only from actual calls and known tool accounting; reset it only at a known new-message boundary. A planning estimate is not quota evidence.

For each join, store outgoing/incoming clip IDs and versions; intended continuous or motivated cut; reference-frame timestamp separately from actual cut points; last retained outgoing and first retained incoming frame indices/timestamps; time units and trim inclusion rules; observed subject/camera motion; issue classification; evidence and rendered-preview path if available; repair count; dialogue/sync checks; and verification gaps. Count repeated attempts on the same join defect toward the existing repair limit, including attempts across regenerated clip versions. A regenerated clip must not silently reset the unresolved defect's retry count. Mark join checks stale when either source version or cut point changes, then update the timeline and subtitle status accordingly.

On resume, read state, confirm referenced files exist, check available tools and whether saved snapshot context remains usable, and continue from the first incomplete step. An expired snapshot does not invalidate a good saved clip; use available approved frames/references and disclose any resulting limitation. Do not regenerate approved work solely because the chat is new.

If the user switches an existing project to automatic mode, disable prior routine review gates and clear waits that existed only for those gates. Preserve actual approvals and completed clips. Continue from the next incomplete step; do not restart or ask the user to reconfirm the mode. Genuine blockers and material script decisions remain pending.
