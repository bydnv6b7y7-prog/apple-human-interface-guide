# Chapter 6: Icons, Images, SF Symbols, and Branding

## Core Idea

Visual assets should make content and action easier to recognize. Use system symbols and rendering behavior when they express the concept; create custom assets only when they add necessary meaning or identity. Brand should live in the quality, voice, color, content, and a few distinctive moments—not compete with the task on every page.

## Frameworks Introduced

### SF Symbols rendering modes

- **Monochrome** — One color applied uniformly.
- **Hierarchical** — One color with varying opacity to communicate visual hierarchy.
- **Palette** — Two or three explicitly assigned colors.
- **Multicolor** — The symbol’s intrinsic colors.

### SF Symbols animation families

Appear, Disappear, Bounce, Scale, Pulse, Variable Color, Replace and Magic Replace, Wiggle, Breathe, Rotate, Draw On, and Draw Off. Choose an effect for feedback or continuity, not spectacle.

### App icon appearances

Maintain a coherent core design across the supported default, dark, clear, and tinted presentations. Provide artwork the system can mask and render; do not pre-bake system effects.

## Key Concepts

### Prefer familiar symbols

Use an SF Symbol when its meaning is established and appropriate. A familiar symbol can work across sizes, weights, appearances, localization, and platform states better than a custom bitmap.

Pair symbols with text when meaning is not obvious, consequences are important, or several neighboring symbols could be confused. Every meaningful symbol needs an accessibility label when the visible text does not already provide it.

### Match symbols to their context

Choose weight, scale, alignment, and detail that harmonize with adjacent text and controls. Account for optical padding rather than forcing every shape to the same visible box. Let system components manage selected and unselected variants where possible.

Use variable color to communicate a changing value or state, not merely depth. Use hierarchical rendering for visual depth and priority. Keep palette and multicolor treatments restrained within dense control areas.

### Animate meaningfully

A symbol may bounce to confirm an action, replace to preserve continuity between two states, pulse for temporary activity, or draw on to reveal progress. Keep the effect brief, interruptible, and consistent. Avoid repeating animation on frequently used controls or using motion as the sole status cue.

### Create custom symbols as members of the system

Start from Apple’s symbol templates so alignment, baseline, weights, and scale behave predictably. Preserve a consistent perspective and stroke language. Supply alternative text. Do not reproduce Apple products, protected marks, or familiar system symbols with changed meaning.

### Treat images as content

Use the correct resolution for the display scale, preserve aspect ratio unless cropping is intentional, include an appropriate color profile, and test on real devices. If an image initiates an action, put it inside a Button or another semantic control instead of attaching an invisible gesture to a passive image view.

Text over imagery needs a stable contrast strategy such as controlled composition, a system material, or a deliberate overlay. Do not assume every image provides the same readable region.

### Express brand with restraint

Use a coherent accent, voice, imagery style, illustration, custom display type, motion signature, or content treatment. Keep navigation and common controls familiar. Avoid repeating the logo in toolbars, empty states, and every page title.

The launch screen should create continuity with the first interface, not act as an advertisement or logo interstitial.

### Build app icons for recognition

Keep the primary concept centered and legible at small sizes. Prefer vector-origin artwork and simple forms. Avoid photographs, screenshots, excessive text, imitation device frames, or tiny interface details. Supply square artwork and let the system apply masks and appearance effects.

Alternate icons should remain closely related to the app’s identity; they are variations, not unrelated promotional art.

## Mental Models

### Recognition before expression

For functional icons, optimize in this order:

1. Does the concept read?
2. Does it match platform convention?
3. Does it remain clear at the actual size and state?
4. Does it harmonize with adjacent content?
5. Only then, does it express brand?

### Asset or component

If people can act on it, model it as a control with a semantic role, state, hit region, focus behavior, and accessibility label. Its visible image is only one part of the component.

### The silhouette test

Inspect an app icon and custom functional icon at small size, in monochrome, and without internal detail. If the primary concept disappears, simplify.

## Anti-patterns

- Unlabeled custom icons for important or destructive actions.
- Mixing filled, outlined, photorealistic, and mismatched-perspective icons in one control group.
- Hard-coded symbol sizes that misalign with text styles.
- Colorful animated symbols competing inside a toolbar.
- Giving a custom icon the silhouette of a known system action but a different result.
- Adding tap gestures directly to images without button semantics.
- Embedding text in images that must localize or scale.
- Repeating the logo on every page.
- Using the launch screen as a timed brand splash.
- App icons containing screenshots, tiny words, device frames, or system-added effects baked into the art.

## Implementation Bridge

- Use SwiftUI Image with systemName, Label, Button, and symbol rendering/effect APIs.
- Let font and image scale coordinate symbol metrics with nearby text.
- Use asset catalogs for scale variants, appearance variants, wide-gamut assets, and app-icon resources.
- Prefer vector PDF or SVG source where the platform workflow supports it, then verify rasterization at actual sizes.
- Add accessibility labels to symbol-only controls and hide purely decorative images from assistive technologies.
- Snapshot-test symbols at normal, selected, disabled, increased-contrast, and right-to-left states.

## Reference Table

| Need | First choice | Use custom work when |
| --- | --- | --- |
| Common action | Familiar SF Symbol | No symbol communicates the domain concept |
| Selected state | System component state or filled variant | The product has a tested domain-specific state |
| Depth within one symbol | Hierarchical mode | Separate semantic colors are truly needed |
| Multiple semantic parts | Palette or Multicolor | The colors remain legible and meaningful |
| Branded identity | Accent, voice, imagery, app icon | It does not displace task content |
| Tappable image | Semantic Button containing Image | Never a bare image with hidden interaction |

## Worked Example: Habit Tracker

The concept gives each habit a bespoke colored line icon, animates all icons continuously, places the logo in every navigation bar, and overlays white labels on user photos.

Reconstruct it:

1. Map common concepts to SF Symbols and keep a small custom set only for domain-specific habits.
2. Use a consistent rendering mode and weight; pair unfamiliar symbols with text.
3. Animate only the checked habit, using a brief effect that reinforces completion and respects Reduce Motion.
4. Remove repeated logos and express identity through the app accent, illustration style, copy, and the app icon.
5. Put photo labels on a stable material or dedicated text region.
6. Implement each habit row as a semantic control with a 44-point-or-larger hit region and an accessible state such as “Completed.”

## Key Takeaways

- Prefer familiar SF Symbols and system state behavior.
- Match symbol weight, alignment, rendering, and animation to context.
- Treat every interactive image as a semantic control.
- Keep brand expression coherent but subordinate to content and action.
- Make app icons simple, recognizable, and system-ready.

## Connects To

- Chapter 4: Color, Materials, and Dark Mode
- Chapter 7: Accessibility, Privacy, and Localization
- Chapter 8: Motion, Feedback, and Haptics
- Chapter 11: Buttons, Menus, Toolbars, and Actions

## Source Focus

SF Symbols; Icons; Images; App icons; Branding; Motion; Accessibility; Buttons.
