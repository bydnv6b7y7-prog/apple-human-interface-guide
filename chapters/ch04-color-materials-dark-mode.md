# Chapter 4: Color, Materials, and Dark Mode

## Core Idea

Color and material communicate hierarchy, state, and separation. They should adapt with the system, remain legible in real conditions, and never become the only carrier of meaning. On current Apple platforms, content and controls often occupy distinct visual layers; restraint keeps that separation understandable.

## Frameworks Introduced

### Semantic color system

Choose color by role rather than by a fixed RGB value:

- Label and secondary-label roles.
- Background, grouped-background, fill, separator, and tint roles.
- Status roles such as success, warning, and destructive.
- App accent roles used consistently for interactivity or brand expression.

Semantic and asset-catalog colors can resolve for Light Mode, Dark Mode, increased contrast, and platform context.

### Content layer and control layer

Current Apple visual design uses translucent, system-managed materials to distinguish controls and navigation from content. Think in two layers:

- **Content layer:** information, imagery, documents, lists, media, and app-specific surfaces.
- **Control layer:** navigation, toolbars, tab bars, and controls that act on content.

Use system effects to establish this relationship. Do not recreate material appearance with fixed opacity, blur, borders, and shadows.

## Key Concepts

### Assign one meaning to each color

If blue means “interactive,” avoid also using the same blue for passive decoration. If red means destructive or critical, do not use it as a routine accent. Consistent meaning reduces the need for labels and protects recognition across the app.

### Color is reinforcement

Every important state needs another cue: text, symbol, shape, position, pattern, or accessibility value. A red field border alone does not explain an error; pair it with an actionable message and an accessible announcement.

### Use system colors where their meaning fits

System colors automatically adapt to appearance and accessibility settings. Avoid hard-coding their visual values or redefining familiar meanings. For custom brand colors, provide light, dark, and increased-contrast variants and test them as foreground and background combinations.

### Honor the system appearance

Support Dark Mode unless the content has a strong, task-specific reason to remain in one appearance, such as a media-viewing environment. Avoid adding an app-specific appearance switch that competes with the person’s system preference.

Dark Mode is not color inversion. Re-evaluate:

- Contrast and visual weight.
- Elevated surfaces and separators.
- Image assets and shadows.
- Saturated accents that vibrate on dark backgrounds.
- Transparency over unpredictable content.

### Use material to clarify depth, not decorate

System materials adapt to wallpaper, content, contrast settings, and platform rendering. Prefer the standard bar, sheet, popover, and control treatments. Avoid stacking many translucent panels or tinting each control independently; the result weakens hierarchy and becomes noisy over colorful content.

### Keep Liquid Glass restrained

Use color in the control layer primarily for status or one high-priority action. When content is already colorful, monochrome toolbars and tab bars often keep attention where it belongs. Prefer a coherent tint or background role over giving each label a different color.

### Test contrast in context

For custom foreground/background pairs, meet at least 4.5:1 for ordinary text and strive toward 7:1 where feasible. Also test Increase Contrast and Reduce Transparency. Numerical contrast is necessary but not sufficient: thin type, glare, blur, motion, and image variation can still reduce readability.

## Mental Models

### Meaning, adaptation, contrast

Approve a color only when:

1. Its semantic meaning is unambiguous.
2. It adapts to all supported appearances and states.
3. Its contrast remains sufficient in the real composition.

### The translucency test

Ask what appears behind the material at the brightest, darkest, and busiest points. If text or controls become unstable, use a system treatment with stronger separation, adjust the underlying content, or choose an opaque semantic surface.

### The grayscale test

Temporarily remove saturation. If selection, error, hierarchy, or interactivity disappears, the design relies too heavily on color.

## Anti-patterns

- Fixed black, white, or gray values standing in for semantic system colors.
- A color that means both selection and warning.
- Color-only status dots with no label or accessible value.
- App-level Light/Dark controls that override system preference without a task need.
- Custom blur recipes that imitate system materials.
- Translucent cards nested inside translucent cards.
- Brightly tinting every toolbar item and tab over colorful content.
- Using low-opacity text to manufacture hierarchy at the cost of legibility.
- Placing text directly over an image without a reliable contrast strategy.

## Implementation Bridge

- Use SwiftUI Color semantic values and named colors from asset catalogs with appearance variants.
- Express interaction tint at a coherent container level rather than styling every descendant.
- Use system materials, toolbar backgrounds, sheet presentation, and standard controls.
- Query accessibility settings only to adapt behavior; do not override them.
- Provide symbols, labels, selected states, and accessibility values alongside status color.
- Test screenshots in both appearances, increased contrast, reduced transparency, grayscale, and over representative content.

When custom colors are essential, document each token by semantic role: for example, surfacePrimary, textSecondary, actionAccent, statusCritical. Do not name product tokens “lightGray” or “brandBlue600” in page-level code unless the design-system layer maps them to meaning.

## Reference Table

| Need | Preferred treatment | Avoid |
| --- | --- | --- |
| Primary action | One coherent accent or prominent system style | Multiple competing accent colors |
| Destructive action | Destructive semantic role plus explicit label | Red as general decoration |
| Selection | Standard selected state plus symbol/text/shape | Color change alone |
| Navigation over content | System bar/material and edge behavior | Hand-built blur overlay |
| Text over image | Stable overlay/material or controlled image region | Assuming every image has dark corners |
| Dark appearance | Semantic colors and adapted assets | Mechanical inversion |

## Worked Example: Finance Dashboard

The draft uses green for gains, red for losses, blue for selected accounts, and translucent cards over a multicolor chart. Values are distinguishable only by hue.

Reconstruct it:

1. Keep gain/loss color but pair each value with a sign, label, and directional symbol.
2. Represent account selection with the standard selected row state and checkmark, not blue text alone.
3. Move the chart to the content layer; use a stable semantic background for numeric summaries.
4. Let the navigation and toolbar use system material with restrained monochrome controls.
5. Reserve the accent for the primary “Add Transaction” action.
6. Supply light, dark, and increased-contrast chart tokens and ensure adjacent series remain distinguishable by line style or marks.
7. Verify both appearances, Reduce Transparency, Increase Contrast, and grayscale.

The design keeps financial semantics while remaining readable and structurally calm.

## Key Takeaways

- Choose color by semantic role and keep its meaning consistent.
- Never use color as the only signal.
- Honor system appearance and accessibility settings.
- Keep content and control layers visually distinct with system treatments.
- Use translucent materials sparingly and test them over real content.

## Connects To

- Chapter 3: Layout and Adaptivity
- Chapter 6: Icons, Images, and Branding
- Chapter 7: Accessibility, Privacy, and Localization
- Chapter 19: State, Status, and Progress

## Source Focus

Color; Dark Mode; Materials; Accessibility; Branding; Images; Buttons; Tab bars; Toolbars.
