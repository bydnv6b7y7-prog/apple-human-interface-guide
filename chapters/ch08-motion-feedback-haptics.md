# Chapter 8: Motion, Feedback, Haptics, and Loading

## Core Idea

Feedback closes the loop between action and result. Motion, sound, haptics, state changes, and progress indicators should explain cause, continuity, status, or consequence. They should be brief, interruptible, accessible, and proportionate to the event.

## Frameworks Introduced

### Four jobs of motion

- **Continuity:** Show where content came from or went.
- **Causality:** Connect an action to its result.
- **Status:** Communicate progress, change, or availability.
- **Focus:** Direct attention to a meaningful moment.

### Feedback ladder

Choose the least interruptive feedback that reliably communicates the event:

1. Immediate visual state change.
2. Inline label, symbol, or progress.
3. Brief symbol motion or haptic.
4. In-app banner or transient notice.
5. Modal alert only for critical, actionable interruption.
6. Notification only when the app is not the right foreground context.

## Key Concepts

### Make the interface respond immediately

Every interaction needs prompt evidence: press state, selection, navigation transition, content update, or progress. If the underlying work takes time, acknowledge the action immediately and then reveal honest progress.

### Match physical expectation

Motion should follow the gesture and preserve spatial relationships. Dragged content follows the pointer or touch. A pushed detail appears connected to its source. Dismissal reverses the transition or exits in the expected direction. Unrelated zooms, spins, or bounces break causality.

### Keep common interactions fast

Frequent controls should not make people wait through custom choreography. System components already supply familiar press, navigation, presentation, and selection motion. Add custom movement only when it explains a product-specific relationship.

### Let people interrupt

A person should be able to reverse a gesture, dismiss a transition, scroll during loading when safe, or cancel a long operation. Animation should respond to current state rather than finish a stale sequence after the person has moved on.

### Respect Reduce Motion

When Reduce Motion is enabled:

- Replace large zoom and scale transitions with fades or direct state changes.
- Reduce parallax, peripheral travel, looping, and repeated animation.
- Keep essential progress and state information visible without movement.
- Do not simply slow every animation; slower large motion can be more uncomfortable.

### Use haptics as reinforcement

Use standard haptic meanings for selection, success, warning, and error where they fit. Keep the relationship between cause and feedback immediate and consistent. Haptics should complement visible or audible information and remain short and discrete.

Avoid haptics for routine scrolling, decorative events, every tap, or background changes. Respect device capability and user settings.

### Coordinate sound carefully

Sound can confirm an important event or provide spatial and temporal information, but it must respect silent mode, output route, volume, and interruptions. Never use sound as the only notification of success, failure, or danger.

### Represent waiting honestly

For work with measurable duration, use determinate progress. For brief or initially unknown work, use an indeterminate indicator, then change to determinate when reliable progress becomes available. Do not fake smooth progress or reset it unexpectedly.

Keep the indicator near the affected content, preserve its position, and offer Cancel or Pause for long operations when safe. A loading screen is justified only when content cannot yet be useful; for media, use a minimal treatment if startup takes more than roughly two seconds.

## Mental Models

### Cause, path, rest

For each transition define:

1. **Cause:** What action or state change starts it?
2. **Path:** What spatial or semantic relationship does it explain?
3. **Rest:** What stable state remains when it ends?

If the path explains nothing, a direct change or subtle fade is often better.

### Event weight

Match feedback weight to consequence:

- Row selection: visible selection.
- Toggle: state change, optional selection haptic.
- Saved draft: inline status.
- Completed meaningful task: concise confirmation, perhaps a success haptic.
- Irreversible destructive failure: clear message and recovery, possibly alert.

### Persistent truth

Transient animation or haptic can call attention to a change, but the final state must remain inspectable. A checkmark that flashes and disappears without updating the row leaves no durable truth.

## Anti-patterns

- Decorative animation attached to every screen entrance.
- Long, noninterruptible transitions.
- Spring or bounce effects that conflict with the gesture’s direction.
- Slowing motion instead of reducing it for Reduce Motion.
- Haptics on every tap or scroll tick.
- Custom haptic patterns for meanings already served by standard feedback.
- Spinner with no context during a long operation.
- Fake determinate progress or a bar that moves backward without explanation.
- Using a notification for an error the person is already viewing.
- Relying on a brief toast as the only record of an important state.

## Implementation Bridge

- Use system navigation, sheet, menu, control, and symbol effects before custom animation.
- Drive animation from a single source of truth and support cancellation when state changes.
- Read the accessibility Reduce Motion environment and provide a simpler transition.
- Use sensory feedback APIs or platform haptic generators for standard semantics; avoid starting the haptic engine for ornamental events.
- Use ProgressView for standard progress presentation and expose progress through accessibility values.
- Pause animation and expensive effects when content is offscreen or the app becomes inactive.
- Test on real hardware: simulator timing does not represent touch latency, haptics, audio routing, or rendering cost.

## Reference Table

| Situation | Appropriate feedback |
| --- | --- |
| Button press | Immediate press state and resulting state change |
| Selection change | Persistent selected state; optional selection haptic |
| Reordering | Direct manipulation plus destination feedback |
| Short unknown task | Indeterminate ProgressView near affected content |
| Long measurable task | Determinate progress with cancel/pause when possible |
| Success | Persistent updated state; restrained confirmation |
| Error | Local actionable message; alert only when interruption is necessary |
| Background completion | Notification only if timely and useful outside the app |

## Worked Example: File Upload

The draft disables the whole screen, plays a looping branded animation, shows “Uploading…,” and emits a strong haptic when finished.

Reconstruct it:

1. Insert the file immediately in the destination list with an uploading state.
2. Show determinate row-level progress when bytes are known; begin indeterminate only during preparation.
3. Allow other safe work to continue and offer Cancel on the uploading item.
4. Preserve a failed row with an actionable Retry state rather than presenting a generic alert.
5. Use a concise success state and a light, standard haptic only if completion is meaningful while the person remains engaged.
6. If the app backgrounds and completion remains useful, consider one notification without sensitive file details.
7. Under Reduce Motion, remove any traveling or scaling flourish while keeping progress visible.

## Key Takeaways

- Use feedback to explain cause, continuity, status, and consequence.
- Choose the least interruptive channel that reliably communicates the event.
- Keep motion brief, physically coherent, interruptible, and Reduce-Motion-aware.
- Use haptics and sound as reinforcement, never as the only signal.
- Show honest, local, persistent progress and recovery.

## Connects To

- Chapter 6: Icons, Images, and Branding
- Chapter 14: Inputs and Interactions
- Chapter 18: Media and Full-Screen Experiences
- Chapter 19: State, Status, and Progress

## Source Focus

Motion; Feedback; Haptics; Playing audio; Playing video; Progress indicators; Refreshing content; Accessibility.
