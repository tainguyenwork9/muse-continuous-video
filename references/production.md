# Production procedure

## 1. Breakdown and continuity plan

Map every script beat and exact spoken line to planned clips, each approximately ten seconds. Clip boundaries need not equal narrative scene boundaries. Allow breathing room for speech and action; do not cram excess dialogue into a fixed clip. Record planned duration and explain material discrepancies from the requested duration.

Build a compact continuity bible covering character identities and body proportions, face and hair, wardrobe, important props, locations, layout, lighting, time, visual style, and voice descriptions. Assign stable IDs. Separate invariants from changes explicitly required by the script: an approved clothing change, injury, wet surface, or time jump becomes the new state for subsequent relevant scenes.

Prefer continuous camera and action when narratively appropriate. Permit motivated cuts when location, time, or story requires them. Do not force unrelated scenes into a fake single take. Specify screen direction, camera position and movement, object ownership, and the incoming and outgoing action for each clip.

If references are missing, create character and key environment/prop images with available image tools. Useful views include face, full body, and angles needed in the script. Present them at the design review stage when enabled. If image generation is unavailable, explain the limitation and request suitable references or an agreed alternative. Reuse approved references rather than independently redesigning every scene.

For storyboard review, present a frame or available visual reference for each planned shot, exact dialogue, timing, action, and intended connection. Clearly distinguish generated storyboard images from descriptions when only text is available.

## 2. Generate a batch sequentially

Produce approximately three clips per review batch, fewer for the final batch. Sequentially generate dependent clips so each can use the actual preceding output. Respect the tool's per-message limit including retries; never evade it through parallel calls.

For each clip, provide only relevant approved references and a clear prompt containing:

- Visual style, setting, lighting, character and prop identities.
- Initial state, the script beat, and a feasible progression of action.
- Camera framing, motion, and screen direction.
- Exact dialogue and requested speaker/voice characteristics, plus appropriate ambience and music intent.
- Continuity requirements and explicit exclusions for observed failure risks, such as an extra prop or changed wardrobe.

For a continuous boundary, inspect the preceding clip's final usable frames. Choose a clean frame close to the actual intended cut, recording its timestamp. Use it as the next opening reference when supported, together with relevant identity references and supported snapshot context. Describe how the ongoing action continues rather than restarts. If the source frame precedes the clip's end, trim or otherwise align the eventual cut to avoid repeating the intervening action. Do not assume a snapshot ensures matching appearance or motion.

For an intentional cut, preserve narrative and physical state while specifying the new viewpoint or setting. Do not feed a mismatched previous frame as an opening constraint merely because it exists.

Persist each output, actual duration, references, prompt, snapshot identifiers if returned, and verification results immediately. Keep alternate versions separate; never overwrite an approved clip with an unreviewed replacement.

## 3. Inspect, repair, and review

Check each clip and its boundary with the preceding clip before presenting the batch. Use playback when available and inspect representative frames including the beginning, middle, end, and both sides of each join. Check:

- Face, hair, body, wardrobe, approved state changes, and voice identity where audible.
- Prop count, appearance, ownership and position; no unexplained appearance or disappearance.
- Environment geometry, lighting, time, screen direction, and camera trajectory.
- Action continuity, repeated or missing movement, visible jumps, malformed frames, and frozen padding.
- Complete script coverage, exact dialogue, pacing, audible continuity, and mouth synchronization when applicable and inspectable.

Still-frame sampling can reveal appearance errors but cannot prove continuous motion. Audio metadata can establish a track's presence but cannot prove its contents. Use transcription or other inspection tools only if actually available, and distinguish automated findings from direct audiovisual review.

Automatically attempt targeted corrections before presenting known defects. Prefer a corrected prompt, better reference frame, supported snapshot reuse, or harmless edit according to the failure. After three repair attempts for the same unresolved defect without meaningful improvement, pause that branch, explain the issue, and propose a concrete change in angle, timing, transition, or staging for user approval. Do not loop indefinitely. Preserve exact dialogue and story; changes affecting either require approval.

Show the batch with enough preceding footage to judge the first boundary. When enabled, obtain batch approval before starting the next batch. When listening/playback is unavailable, explicitly ask the user to judge speech accuracy, voice, lip synchronization, motion, and audio joins that cannot be verified. If the user waived routine batch review, request a targeted check at the next agreed review point or on the final review export. Never silently treat unverified aspects as passed.

If an upstream clip changes, reassess downstream clips dependent on its end state or snapshot. Mark affected approvals stale; repair only the affected sequence and resubmit where review is enabled.

## 4. Edit and finish

Inspect actual media properties before choosing assembly settings. Match the requested aspect ratio and use achievable resolution/frame rate; do not promise unsupported generation quality or imply upscaling adds native detail.

Remove dead padding or repeated boundary frames and adjust joins when this preserves approved action and every spoken line. Prefer a clean matched cut for continuous action. Crossfades can create double faces or props; do not apply them globally to conceal continuity defects. Substantive restaging requires approval.

Select music and ambience appropriate to the script using available tools/assets. If an appropriate continuous audio bed is available, it can span clip boundaries. Where possible, smooth ambience and balance loudness without overlapping or clipping dialogue. Generated per-clip audio is not automatically a coherent soundtrack. If voice replacement or exact dialogue requires an unavailable audio tool, surface the blocker rather than claiming success. Do not add invented spoken lines.

Use stream-copy concatenation only when media parameters and edit requirements are compatible. Trimming, transitions, audio processing, or incompatible streams may require re-encoding. Follow actual installed FFmpeg/tool instructions. Technical checks verify the container and streams, not narrative quality.

Create UTF-8 SRT subtitles from the final spoken content, retaining the approved wording and language. Derive cue timing from the final edited timeline and actual speech evidence, not simply ten-second boundaries. If speech cannot be inspected or transcribed, label timing/content as provisional and obtain user verification; do not assert alignment based on the script alone. Never rewrite subtitles to conceal incorrect generated dialogue. For a confirmed speech-free script, provide an empty SRT and explain that it has no dialogue cues.

Verify the MP4 is readable, has expected streams, aspect ratio and plausible duration, and contains all approved beats. Verify SRT cues have valid timestamps within the final duration, ordered readable cues, and no accidental overlaps. Check the assembled boundaries and ending, not only the source clips. Record any unverified audiovisual aspects and route them to user review.

Provide final MP4 and SRT download links. Keep project state and intermediate files for resumption; do not include them as extra deliverables unless requested.
