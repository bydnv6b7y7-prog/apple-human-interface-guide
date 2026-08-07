# Chapter 7: Accessibility, Inclusion, Privacy, and Localization

## Core Idea

An iOS page is complete only when people with different abilities, languages, input methods, settings, and privacy expectations can use it with confidence. Accessibility and privacy shape the structure of a feature; they are not compliance layers added after the visual design.

## Frameworks Introduced

### Multiple channels

Communicate important meaning through more than one of:

- Text or accessible description.
- Shape, symbol, position, or pattern.
- Color.
- Motion.
- Sound.
- Haptics.

No critical state should depend on only color, audio, animation, or a gesture.

### Permission in context

Use a four-part permission decision:

1. Is the data or capability necessary?
2. Can the feature work with less access?
3. Is the benefit visible at the moment of the request?
4. Is the usage description specific and honest?

### Logical direction

Build layout with leading/trailing and start/end semantics. Mirror directional interface behavior for right-to-left languages while preserving physical and universal meaning.

## Key Concepts

### Start with perceivability

Use system text styles, semantic colors, strong contrast, and layouts that survive larger text. Aim to support text enlargement to at least 200% where feasible. Avoid truncating essential content. At large sizes, stack controls, reduce columns, and allow scrolling rather than shrinking type.

For custom text/background pairs, meet at least 4.5:1 and aim higher where possible. Test Increase Contrast, Reduce Transparency, Bold Text, and grayscale.

Provide alternative text for meaningful images and concise labels for symbol-only controls. Decorative images should not clutter the accessibility tree.

### Make interaction physically and cognitively reachable

On iOS, provide hit regions at least 44 by 44 points even if the visible glyph is smaller. Keep interactive controls clear of the display edge; the source guidance suggests roughly 12 points of breathing room around controls on bezel devices and 24 points on bezel-less devices.

Prefer simple gestures and provide a visible or accessible alternative for complex gestures. Support:

- VoiceOver.
- Voice Control.
- Full Keyboard Access and keyboard-only operation.
- Switch Control.
- Siri and App Shortcuts where the task benefits.
- Assistive Access for essential, simplified workflows.

Avoid timed dismissal for important information. Provide an explicit way to close or continue.

### Keep order and state coherent

Accessibility traversal should follow the visual and logical reading order. Combine elements only when the resulting announcement is more understandable. Announce name, role, value, state, and available action without repeating visible labels.

Selection, expansion, errors, loading, and disabled states need accessible values or announcements. Do not build a visual toggle that exposes itself as an unlabeled button.

### Respect sensory settings

Honor Reduce Motion by reducing large zooms, scale changes, peripheral motion, and repetitive effects. Honor settings related to flashing content. Caption video, provide transcripts or equivalent text for audio, and pair haptics with visual or audible information.

### Write and depict people inclusively

Use plain, respectful language and imagery that reflects varied people and circumstances without stereotyping. Prefer language people use for themselves and avoid unnecessary labels. Jargon, idioms, humor, and culture-specific metaphors can create both comprehension and localization barriers.

### Minimize data

Ask only for information required by the feature, retain it only as needed, and prefer on-device processing when practical. Use platform authentication, keychain storage, passkeys, and Sign in with Apple rather than custom credential handling. Never store credentials as plain text or imitate system authentication UI.

### Request permission at the moment of value

Do not request a cluster of permissions at launch. Let the person reach the feature, understand the benefit, and initiate the request.

A pre-permission explanation is justified only when the benefit or consequence is genuinely unclear. If used, it should have one neutral Continue or Next action that opens the system prompt. Never create fake Allow/Don’t Allow buttons or pressure language. Tracking explanations must not misrepresent the system choice.

The usage description should be a brief, active, specific sentence connecting the capability to the feature, such as “Allow location access to show nearby pickup points.”

### Localize behavior, not only strings

Plan for longer text, different word order, scripts, calendars, number formats, names, addresses, and plurals. Do not concatenate sentence fragments.

For right-to-left interfaces:

- Align layout to logical reading direction.
- Keep list items internally consistent.
- Mirror navigation arrows, progress direction, and directional controls.
- Do not reverse digits.
- Do not mirror photos, logos, universal symbols, or controls whose meaning is a physical direction.
- Review directional symbols and text-bearing artwork individually.

## Mental Models

### The no-single-channel test

Disable one channel at a time: remove color, mute audio, stop motion, or hide imagery. If the person can no longer understand the important state, add another channel.

### The least-power permission

Choose the narrowest access, lowest precision, shortest duration, and most local processing that still delivers the promised value.

### The unfamiliar user

Review the screen as someone who cannot see its layout, cannot perform its gesture, uses the largest text, reads right to left, and distrusts the permission request. The goal is one coherent product, not separate fallback experiences.

## Anti-patterns

- Treating accessibility labels as the entire accessibility effort.
- Touch targets equal to a 16-point visible icon.
- Color-only charts, validation, or selection.
- Autoplaying flashing or looping motion with no adaptation.
- Requiring drag, swipe, pinch, or long press with no alternative.
- Asking for contacts, camera, microphone, location, and notifications on first launch.
- Fake permission dialogs or manipulative pre-prompts.
- Custom password storage or custom UI that imitates Face ID.
- Hard-coded left/right layout and concatenated localized strings.
- Mirroring every image and symbol mechanically.

## Implementation Bridge

- Use semantic controls first; then add targeted accessibility labels, values, hints, traits, actions, and focus behavior.
- Read Reduce Motion, Differentiate Without Color, contrast, transparency, and text-size environment values where adaptation is needed.
- Use leading/trailing alignment and locale-aware formatters.
- Test VoiceOver rotor order, Voice Control names, Full Keyboard Access, Switch Control, large text, RTL pseudolocalization, and permission-denied flows.
- Use LocalAuthentication, AuthenticationServices, Keychain services, privacy manifests, and system permission APIs.
- Keep sensitive content out of widgets, Live Activities, notifications, logs, screenshots, and app-switcher snapshots as appropriate.

## Reference Table

| Requirement | Design response |
| --- | --- |
| Small visible symbol | Expand its semantic hit region to at least 44 × 44 pt |
| Color status | Add text, symbol, shape, or pattern |
| Audio/video meaning | Add captions, transcript, or equivalent description |
| Complex gesture | Add a standard control or accessible action |
| Large text | Reflow, stack, grow, and scroll |
| Permission | Ask in context with a specific usage description |
| Sensitive authentication | Use system authentication and secure storage |
| RTL | Use logical direction and mirror only directional meaning |

## Worked Example: Nearby Photo Journal

The app requests photo-library, precise location, contacts, microphone, and notifications on launch, then displays a color-only map and custom pinch gesture.

Reconstruct it:

1. Open into a usable journal with sample or existing entries.
2. Ask for selected-photo access when the person chooses Add Photo.
3. Ask for location only if they enable “Attach place,” using reduced accuracy if neighborhood-level context is enough.
4. Do not request contacts until they choose a collaboration feature; do not request microphone unless they start voice notes.
5. Pair map colors with symbols and text; provide an accessible list representation.
6. Add standard zoom controls and accessibility actions alongside pinch.
7. Let text reflow at accessibility sizes and test Arabic layout.
8. Keep location and private photo details out of notification previews and glanceable surfaces.

## Key Takeaways

- Build accessibility, privacy, and localization into feature structure.
- Provide multiple channels for important meaning and alternatives for gestures.
- Support large text, semantic controls, coherent focus, and 44-point hit regions.
- Request the least access at the moment its value is clear.
- Use logical direction and review what should—and should not—mirror.

## Connects To

- Chapter 3: Layout and Adaptivity
- Chapter 4: Color, Materials, and Dark Mode
- Chapter 8: Motion, Feedback, and Haptics
- Chapter 15: System Experiences

## Source Focus

Accessibility; Inclusion; Privacy; Right to left; Layout; Color; Motion; Feedback; Managing accounts; Notifications.
