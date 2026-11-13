# Production procedure

## 1. Breakdown and continuity plan

Map every script beat and exact spoken line to planned clips, each approximately ten seconds. Clip boundaries need not equal narrative scene boundaries. Allow breathing room for speech and action; do not cram excess dialogue into a fixed clip. Record planned duration and explain material discrepancies from the requested duration.

Budget using usable duration after trims, not nominal output length. Before measurements exist, 8–9 usable seconds per ten-second clip is a conservative planning assumption, not an observed tool guarantee or an instruction to trim good footage. At that assumed yield, 60 seconds needs roughly 7–8 clips and at least two messages under the reported six-clip limit, before retries. After each batch, recompute remaining clip needs from measured retained durations and script coverage. Track generation quota separately from review batches; do not add filler merely to meet an estimate.

Choose and record the audio strategy before generating clips:

- Per-clip speech, ambience, and music: retain generated music, inspect joins, and do not automatically add a second music bed.
- Continuous music added during editing: first confirm a suitable asset or generation tool exists; request "dialogue and ambience only, no background music" in every clip prompt.
- Separately produced continuous narration, if an actual voice tool or supplied recording is available: align visuals to that recording and request no generated speech; request no music when adding a separate music bed.

Prompt instructions do not guarantee clean audio. Music mixed with dialogue cannot generally be removed cleanly by simple muting or filtering. Stem separation, if available, may introduce artifacts and requires inspection. If unwanted music is baked into needed speech, regenerate or use an approved replacement audio workflow; do not layer competing beds or silently discard dialogue.

Estimate speech duration before generation. As initial planning heuristics, use roughly 2–2.5 English words/second or 3–4 Vietnamese syllables/second, then calibrate to the selected voice, pauses, names, and actual output. Reserve about 1–2 seconds for breathing/action where needed. For example, seven seconds of speech allows approximately 14–18 English words or 21–28 Vietnamese syllables, not a universal words-per-clip cap. With independently generated clip speech, keep each sentence in one clip where possible to avoid a mid-sentence voice change. If an exact sentence will not fit, seek approval for an audio workflow or script adjustment; do not silently rewrite it. Continuous separately recorded narration may span visual cuts without splitting its audio.

Build a compact continuity bible covering character identities and body proportions, face and hair, wardrobe, important props, locations, layout, lighting, time, visual style, and voice descriptions. Assign stable IDs. Separate invariants from changes explicitly required by the script: an approved clothing change, injury, wet surface, or time jump becomes the new state for subsequent relevant scenes.

Prefer continuous camera and action when narratively appropriate. Permit motivated cuts when location, time, or story requires them. Do not force unrelated scenes into a fake single take. Specify screen direction, camera position and movement, object ownership, and the incoming and outgoing action for each clip.

If references are missing, create character and key environment/prop images with available image tools. Useful views include face, full body, and angles needed in the script. Present them at the design review stage when enabled. If image generation is unavailable, explain the limitation and request suitable references or an agreed alternative. Reuse approved references rather than independently redesigning every scene.

For storyboard review, present a frame or available visual reference for each planned shot, exact dialogue, timing, action, and intended connection. Clearly distinguish generated storyboard images from descriptions when only text is available.

## 2. Generate sequentially to completion

Generate dependent clips sequentially so each can use the actual preceding output, and continue until the script is covered. Do not pause after three clips or ask for routine batch approval. Internal processing batches and checkpoints are bookkeeping, not review gates. Respect the actual per-message limit including retries; never evade it through parallel calls. If explicitly requested, use the user's chosen review cadence instead.

In automatic mode, select and lock reference designs against the script and user constraints without requesting approval. Throughout this procedure, an "approved" reference or beat means a user-approved item where available; otherwise use the internally selected version of the user-provided script/design and record that distinction. Prepare the storyboard internally unless presentation is requested.

For each clip, provide only relevant approved references and a clear prompt containing:

- Visual style, setting, lighting, character and prop identities.
- Initial state, the script beat, and a feasible progression of action.
- Camera framing, motion, and screen direction.
- Exact dialogue and requested speaker/voice characteristics, plus appropriate ambience and music intent.
- Continuity requirements and explicit exclusions for observed failure risks, such as an extra prop or changed wardrobe.

For a continuous boundary, inspect the preceding clip's final usable frames. Choose a clean frame close to the actual intended cut, recording its timestamp. Use it as the next opening reference when supported, together with relevant identity references and supported snapshot context. Describe how the ongoing action continues rather than restarts. If the source frame precedes the clip's end, trim or otherwise align the eventual cut to avoid repeating the intervening action. Do not assume a snapshot ensures matching appearance or motion.

Extract boundary frames as full-resolution PNG without additional lossy encoding; this avoids adding compression loss but cannot recover detail already lost in the source video. Avoid motion-blurred frames when a suitable clean boundary is available. Compare every clip with the original approved identity and environment references as well as its predecessor. Correct drift against those originals rather than adopting a progressively altered face or prop as the new reference.

For continuing motion, inspect several frames around the candidate reference rather than choosing from a still alone. Record subject position, pose/action phase (for example, which foot is planted), direction and approximate speed, plus camera direction, framing and speed. If the tail slows unnaturally, search earlier for a sharp frame with active motion; the last 0.5–1 second can be a starting search region, not a mandatory offset. Prompt the next clip as motion already in progress from its opening, continuing that observed phase and trajectory without a restart or pause. Do not describe an ongoing action as beginning again. These instructions guide generation but do not guarantee velocity or frame matching.

For an intentional cut, preserve narrative and physical state while specifying the new viewpoint or setting. Do not feed a mismatched previous frame as an opening constraint merely because it exists.

Persist each output, actual duration, references, prompt, snapshot identifiers if returned, and verification results immediately. Keep alternate versions separate; never overwrite an approved clip with an unreviewed replacement.

## 3. Inspect, repair, and review

Check each clip and its boundary with the preceding clip before using it as the basis for subsequent clips. Use playback when available and inspect representative frames including the beginning, middle, end, and both sides of each join. Check:

- Face, hair, body, wardrobe, approved state changes, and voice identity where audible.
- Prop count, appearance, ownership and position; no unexplained appearance or disappearance.
- Environment geometry, lighting, time, screen direction, and camera trajectory.
- Action continuity, repeated or missing movement, visible jumps, malformed frames, and frozen padding.
- Complete script coverage, exact dialogue, pacing, audible continuity, and mouth synchronization when applicable and inspectable.

Still-frame sampling can reveal appearance errors but cannot prove continuous motion. Audio metadata can establish a track's presence but cannot prove its contents. Use transcription or other inspection tools only if actually available, and distinguish automated findings from direct audiovisual review.

### Diagnose continuous joins

Inspect a short window on both sides of every intended continuous join, initially about 1–2 seconds per side and wider if needed. Compare ordered frames and normal-speed playback when available. Distinguish:

- A static or slow head/tail that stalls otherwise continuous action.
- Replayed action: the incoming clip returns to an earlier pose, position or camera view and repeats progress already shown.
- A spatial jump, mismatched action phase, direction reversal, or abrupt velocity change despite similar appearance.
- A technical timing defect, such as abnormal presentation timestamp intervals or incompatible media properties.
- An intentional still/map, slow shot, or narrative cut that should not be treated as a defective continuous join.

Freeze detection, frame differences, or motion analysis may locate candidates, but none alone proves a faulty join. Slow ramp-up may evade freeze detection; a deliberate map or still may trigger it. Inspect actual presentation timestamps and stream properties before attributing a stall to concatenation. Uniform timestamps do not prove smooth depicted motion, and re-encoding does not repair replayed action. Record the diagnosis and evidence rather than treating every ten-second boundary as the same defect.

Automatically attempt targeted corrections before presenting known defects. Prefer a corrected prompt, better reference frame, supported snapshot reuse, or harmless edit according to the failure. After three repair attempts for the same unresolved defect without meaningful improvement, pause that branch, explain the issue, and propose a concrete change in angle, timing, transition, or staging for user approval. Do not loop indefinitely. Preserve exact dialogue and story; changes affecting either require approval.

If the tool refuses a generation for policy reasons, record the affected beat and the stated reason without speculating. Stop retrying that refused request; offer compliant alternatives, such as different staging or off-screen action, for user approval when available. Do not silently change the script or disguise a prohibited request to evade the restriction. Track refusals separately from defect repairs; they may still consume tool quota or credits according to the actual service behavior.

In automatic mode, save inspection results and proceed without requesting batch approval. Carry unavailable checks forward to the final delivery, identifying speech accuracy, voice, lip synchronization, motion, or audio joins that remain unverified. Only when the user explicitly enables intermediate review, show the requested previews with enough preceding footage to judge each boundary and wait at those requested gates. Never silently treat unverified aspects as passed.

If an upstream clip changes, reassess downstream clips dependent on its end state or snapshot. Mark affected approvals stale; repair only the affected sequence and resubmit where review is enabled.

## 4. Edit and finish

Inspect actual media properties before choosing assembly settings. Match the requested aspect ratio and use achievable resolution/frame rate; do not promise unsupported generation quality or imply upscaling adds native detail.

Remove dead padding or repeated boundary frames and adjust joins when this preserves approved action and every spoken line. Prefer a clean matched cut for continuous action. Crossfades can create double faces or props; do not apply them globally to conceal continuity defects. Substantive restaging requires approval.

### Repair the pair of cut points

Choose the outgoing and incoming cut points together. Match subject position, pose/action phase, framing, direction and velocity across the cut; do not optimize each clip independently. If the incoming clip replays action, seek a later incoming point that continues the actual outgoing state, or adjust the outgoing point to a compatible earlier state without losing required action. A near-identical still is not sufficient if surrounding movement restarts or reverses.

Remove a static head/tail only after checking that it is unintended. Skipping a moving head can remove real travel and create a jump. Do not automatically remove 0.5 seconds from every head or one second from every tail. Likewise, remove a duplicated boundary frame only when observed: the generated opening may differ from its reference. Record exact source frame indices or timestamps for the last retained outgoing and first retained incoming frames, with explicit inclusive/exclusive trim conventions, to prevent duplication or gaps caused by ambiguous cut times.

Try small frame-level adjustments within the existing repair limit, render the join, and inspect it again with surrounding footage. Protect speech, important actions, and audiovisual synchronization. If the only visually matching cut would remove dialogue or a required beat, regenerate the affected clip or use an available authorized audio workflow; do not silently sacrifice content. Regeneration must reuse the original references and corrected motion description. If a continuous match remains unavailable, prefer a motivated cut that preserves the script and permitted camera choices over forced continuity. Ask only if it changes material content, violates an explicit single-take requirement, or the unresolved repair limit has been reached.

For frame-accurate filtered edits, re-encode with compatible dimensions, sample aspect ratio, pixel format, the project's chosen frame rate, and reset segment timestamps. Handle missing audio explicitly and align intended audio/video segment lengths; do not blindly address an absent audio stream or force 24 fps on every project. Preserve externally continuous narration separately when appropriate. Recheck timestamps and sync after assembly. Do not apply interpolation globally: short local interpolation is a last resort only when inspection can rule out face, hand, or prop distortions. Continuous ambience can support a cut but is not evidence that a visual jump has been fixed.

After changing any cut, recalculate retained duration, downstream timeline offsets, subtitle timing, and remaining footage needs. Recheck affected dependencies if the generated content or reference state changed. Save both cut points and their verification status automatically without introducing a routine user review gate. If playback is unavailable, perform feasible checks, mark motion smoothness unverified, and disclose that with the export.

Select music and ambience appropriate to the script using available tools/assets. If an appropriate continuous audio bed is available, it can span clip boundaries. Where possible, smooth ambience and balance loudness without overlapping or clipping dialogue. Generated per-clip audio is not automatically a coherent soundtrack. If voice replacement or exact dialogue requires an unavailable audio tool, surface the blocker rather than claiming success. Do not add invented spoken lines.

Follow the audio strategy selected before generation. Audio crossfades may smooth compatible ambience but must not overlap spoken words or introduce duplicate music. If no delivery loudness target is specified, a working mix target for an online video can be about -14 LUFS integrated with true peak no higher than -1 dBTP; this is an optional production target, not a universal platform requirement. When measurement tools are available, measure the assembled soundtrack, normalize if appropriate using the available FFmpeg loudnorm workflow (prefer measured two-pass processing), and remeasure the encoded output. Do not claim loudness compliance without measurements or force a silent track to a speech target.

Use stream-copy concatenation only when media parameters and edit requirements are compatible. Trimming, transitions, audio processing, or incompatible streams may require re-encoding. Follow actual installed FFmpeg/tool instructions. Technical checks verify the container and streams, not narrative quality.

Create UTF-8 SRT subtitles from the final spoken content, retaining the approved wording and language. Derive cue timing from the final edited timeline and actual speech evidence, not simply ten-second boundaries. If speech cannot be inspected or transcribed, produce provisional subtitles from the script and final timeline, explicitly disclose their unverified content/timing at delivery, and request verification there without blocking export. Do not assert alignment based on the script alone. Never rewrite subtitles to conceal incorrect generated dialogue. For a confirmed speech-free script, provide an empty SRT and explain that it has no dialogue cues.

Verify the MP4 is readable, has expected streams, aspect ratio and plausible duration, and contains all approved beats. Verify SRT cues have valid timestamps within the final duration, ordered readable cues, and no accidental overlaps. Check the assembled boundaries and ending, not only the source clips. Record any unverified audiovisual aspects and route them to user review.

Provide final MP4 and SRT download links. Keep project state and intermediate files for resumption; do not include them as extra deliverables unless requested.
