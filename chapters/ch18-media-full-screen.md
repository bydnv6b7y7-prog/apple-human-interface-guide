# Chapter 18: Media, Audio, Video, Full Screen, and Immersive Experiences

## Core Idea

Media should preserve the content’s integrity and respect the person’s device, environment, attention, and control. Use system playback behavior, enter full screen only for meaningful benefit, and make interruption, captions, loading, output routing, and exit behavior part of the design.

## Frameworks Introduced

### Media states

- Ready or poster.
- Preparing or buffering.
- Playing.
- Paused.
- Seeking or scrubbing.
- Interrupted.
- Background or Picture in Picture.
- Completed or resumable.
- Failed with recovery.

### Immersion ladder

1. Inline media within the page.
2. Expanded player that retains navigation context.
3. Full-screen media with familiar controls and exit.
4. Platform-specific immersive experience only when presence materially improves the content.

## Key Concepts

### Prefer the system player

Use standard playback controls and behaviors unless the product has a specialized media need. People expect play/pause, seeking, elapsed and remaining time, captions, output routing, volume behavior, full screen, Picture in Picture where applicable, and keyboard or remote support.

Do not repurpose media buttons or system transport controls. Keep controls discoverable across touch, pointer, keyboard, remote, and assistive inputs.

### Preserve the media

Display video at its original aspect ratio. Crop only when the editorial intent and context allow it, and avoid stretching. Use a poster or thumbnail related to the actual content.

For audio, show useful title, creator, artwork, progress, and current output where relevant. Do not make people infer what is playing from artwork alone.

### Respect audio context

Choose the appropriate audio-session behavior. Ordinary interface sounds should respect Silent Mode. Media playback may continue according to explicit user intent, but must respect volume, headphone routing, AirPlay, interruptions, and other audio.

Avoid mixing streams that compete. Pause, duck, or resume according to content and system conventions. Use the system volume view rather than an app-specific control for device output volume.

### Make loading minimal and honest

Show the first useful frame as soon as possible. If startup exceeds roughly two seconds, a minimal black or content-matched state with a standard indicator can preserve focus. Avoid branded loading sequences and misleading progress.

Keep buffering distinct from paused and failed states. If recovery requires action, state it clearly and preserve the playback position.

### Resume where expected

Remember the previous position for long-form content and restore it when that supports intent. After interruption, resume automatically only when system convention and the person’s likely expectation support it; otherwise remain paused with context intact.

### Enter full screen for content, not cleanup

Use full screen when removing surrounding interface materially improves viewing, capture, editing, gameplay, or concentration. Do not use it to avoid solving a crowded page.

Keep essential controls revealable with a familiar gesture and make exit obvious. Let the person choose when to enter and leave. Transition smoothly so the source and destination feel connected.

### Keep overlays controlled

Text, transport controls, and interactive overlays need reliable contrast and safe-area placement. When an interactive overlay appears during playback, pause when necessary; source guidance suggests allowing at least about half a second before requiring interaction so the transition is perceivable.

Avoid covering subtitles, faces, controls, or the content’s focal region. Let transient chrome recede without making essential status impossible to retrieve.

### Support captions and alternatives

Provide captions, subtitles, transcripts, audio descriptions, and accessible control labels as the content requires. Preserve chosen caption and language preferences. Do not rely on sound or visual animation alone to communicate an event.

### Use Picture in Picture for continuity

For eligible video, Picture in Picture lets people continue viewing while navigating elsewhere. Preserve playback state, controls, and a route back to the exact content. Do not misuse it for promotional loops or content that needs constant focused interaction.

## Mental Models

### Content, control, context

- **Content** should stay visually primary.
- **Controls** should be available when needed and recede when not.
- **Context** such as title, position, output route, and interruption state should remain recoverable.

### Interruption matrix

Define behavior for calls, alarms, route changes, app backgrounding, other audio, headset disconnect, network loss, and external playback. For each, specify pause/continue, visible state, persistence, and resumption.

### User-initiated continuation

The more explicit the play action, the stronger the case for continuing through ordinary app navigation. Autoplayed or incidental media should stop more readily.

## Anti-patterns

- Custom player missing captions, output routing, seeking, or accessibility.
- Stretching video or cropping important content by default.
- Interface sound ignoring Silent Mode.
- Custom slider controlling system output volume.
- Autoplaying audio unexpectedly.
- Full-screen mode with hidden or unconventional exit.
- Branded loading animation before every clip.
- Buffering represented as paused or frozen content.
- Overlay controls covering subtitles or essential imagery.
- Resuming loudly after an interruption without context.

## Implementation Bridge

- Use VideoPlayer or AVPlayerViewController for standard playback and AVFoundation for specialized needs.
- Configure AVAudioSession by media purpose and handle route/interruption notifications.
- Use the system route picker and volume behavior.
- Provide timed-text tracks, captions, transcripts, and accessible transport labels.
- Support Picture in Picture through platform APIs where content qualifies.
- Persist media identity and position carefully; avoid storing sensitive viewing state unnecessarily.
- Test Silent Mode, Bluetooth and wired route changes, AirPlay, phone interruptions, backgrounding, network changes, captions, Reduce Motion, and every input method.

## Reference Table

| Need | Preferred behavior |
| --- | --- |
| General video playback | System player and controls |
| Long-form resume | Restore prior meaningful position |
| Startup delay over ~2 seconds | Minimal standard loading state |
| Device volume | System volume UI |
| Full-screen entry | Person-controlled and purpose-driven |
| Full-screen exit | Familiar visible/revealable control and gesture |
| Continue while multitasking | Picture in Picture when appropriate |
| Spoken information | Captions/transcript or equivalent |

## Worked Example: Learning Video

The draft autoplays with sound, uses a custom full-screen player, hides exit until a two-finger tap, overlays a quiz over captions, and restarts after every interruption.

Reconstruct it:

1. Show a relevant poster and begin playback through a clear user action.
2. Use the system player or reproduce its complete transport, caption, route, keyboard, and accessibility behavior only if the learning task truly requires customization.
3. Put a familiar close/full-screen control in a safe region and preserve a standard reveal gesture.
4. Pause before showing the quiz, keep captions unobstructed, and provide enough time to perceive the transition.
5. Save progress and answer state; after an interruption, remain paused with an obvious Resume action unless automatic continuation is clearly expected.
6. Offer transcript and caption choices and support Picture in Picture for passive lesson portions.

## Key Takeaways

- Use system playback behavior and preserve original media presentation.
- Respect Silent Mode, routing, interruptions, captions, and chosen control.
- Make loading, paused, buffering, failure, and resume states distinct.
- Enter full screen only when content benefits and keep exit familiar.
- Define the complete interruption matrix and test it on real hardware.

## Connects To

- Chapter 7: Accessibility, Privacy, and Localization
- Chapter 8: Motion, Feedback, and Haptics
- Chapter 13: Modality and Presentation
- Chapter 19: State, Status, and Progress

## Source Focus

Playing audio; Playing video; Going full screen; Immersive experiences; Media players; Haptics; Motion; Multitasking; Accessibility.
