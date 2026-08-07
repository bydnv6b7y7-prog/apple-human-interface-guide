# Chapter 13: Modality, Alerts, Sheets, Popovers, and Windows

## Core Idea

Presentation changes attention and context. Inline content preserves flow; a popover provides brief contextual capability; a sheet isolates a short task; full screen supports deep focus; an alert interrupts for critical action; a separate window preserves an independent work context. Use the least disruptive presentation that serves the task.

## Frameworks Introduced

### Presentation escalation

1. Inline update, disclosure, or navigation.
2. Popover for a few temporary, related controls in wide space.
3. Sheet for a distinct, short task.
4. Full-screen presentation for immersive content or a complex focused task.
5. Alert for critical, immediately actionable information.
6. Separate window for an independent task or document whose context should persist.

### Modal value test

Modality is justified when it:

- Ensures a person receives critical information and can act.
- Helps confirm or modify a recent action.
- Supports a distinct, narrowly scoped task without losing the parent context.
- Creates necessary focus or an immersive experience.

## Key Concepts

### Use modality only for a clear benefit

A modal experience suspends the parent context and requires dismissal. Keep it simple, short, and streamlined. Avoid building a miniature app with several branches inside a sheet. If subviews are necessary, provide one clear path and keep dismissal controls distinct from internal navigation.

For complex, prolonged work, use a full-screen task, dedicated content flow, or separate window. For supplementary controls that affect visible content, prefer a nonmodal inspector, split region, or appropriately sized sheet.

### Always make dismissal obvious

Follow platform conventions: a clear toolbar button and, where appropriate, swipe-down dismissal. If the task has a Done action, pair it with Cancel or Back when leaving without completion is meaningful.

Before dismissing unsaved user-generated content, preserve it automatically or present proportionate choices such as Save Draft, Discard Changes, and Continue Editing. Do not disable familiar dismissal gestures without explaining or providing a clear route out.

### Present one modal at a time

Close the current modal before showing another. An alert may appear above a modal, but never show more than one alert. Stacked sheets and popover cascades increase cognitive load and obscure the return path.

### Size sheets to the task

Use a sheet for a focused task whose relationship to the parent remains useful. On iPhone, a medium detent can support progressive disclosure only when the content is genuinely usable at that height. Provide a grabber when resizability needs to be apparent and ensure the fully expanded state remains coherent.

On iPad, page- or form-sized sheets often preserve context better than full-screen presentation. Use a full-screen style when the task needs deep focus, complex editing, camera/media, or a large multistep surface.

### Use alerts sparingly

Alerts are for critical information requiring immediate attention or action. Do not use one merely to announce information, routine startup state, an undoable common deletion, or a foreground network issue that can be shown inline.

Alert content:

- A specific title explaining the situation; avoid “Error” and codes.
- Optional brief informative text only when it adds value.
- Up to three concise actions.
- A text field only when input is required to resolve the situation.

Label actions with one- or two-word outcomes such as “Delete,” “Reply,” or “View All.” Use “OK” only for a purely informational alert; prefer result-specific labels and avoid Yes/No. Always label the canceling action “Cancel.” If a destructive choice exists, provide a safe Cancel path and do not make Cancel the default.

On iOS and iPadOS, use an action sheet or confirmation dialog—not an alert—when offering choices related to an intentional action, such as saving or discarding an edited draft. Keep content short enough to avoid scrolling at large text sizes.

### Use popovers for temporary context

A popover should contain a small amount of information or a few related tasks and point clearly to the element that revealed it. Avoid covering the source or essential content.

Normally let selection or tapping outside dismiss it. Include Done or Cancel only when confirmation, multiple selection, or potential data loss makes that clearer. Automatically save work if a nonmodal popover can close by tapping outside; discard only through an explicit Cancel.

Show one popover at a time, never cascade popovers, and do not present another view over one except an alert. On compact iOS layouts, adapt the same content to a sheet or full available space.

### Create windows for durable parallel context

Support multiple windows when people benefit from keeping independent documents or tasks open. Do not open a new window for every detail. Offer the command in an expected context menu or menu, restore state, adapt to resizing, and use system window chrome. In product copy, call it a window rather than exposing implementation terminology such as “scene.”

## Mental Models

### Interruption budget

Every sheet and alert spends context. Inline feedback costs little; an alert costs much more. The more frequent the event, the less interruptive its presentation should usually be.

### Task boundary

Use a sheet when the task has a clear start, short internal path, and obvious return. Use navigation when it belongs to the app hierarchy. Use a window when the context should survive beside other work.

### Save or ask

If work can be preserved safely, save it. If closing creates irreversible loss or ambiguity, ask with specific outcomes. Do not repeatedly ask about reversible, intentional actions.

## Anti-patterns

- Showing a sheet because a page looks crowded without fixing hierarchy.
- Several navigation branches inside a modal.
- Sheet over sheet over sheet.
- Alert on launch for network state, release notes, or promotion.
- Alert for every deletion even when undo exists.
- Vague actions such as Yes, No, or OK for consequential decisions.
- A popover containing a full settings page or warning.
- Unsaved popover edits lost by tapping outside.
- Popovers in compact layouts that obscure most content.
- Opening a new window for transient detail.

## Implementation Bridge

- Use sheet, fullScreenCover, presentation detents, confirmationDialog, alert, and popover modifiers according to semantics.
- Use interactive dismissal control only when loss prevention truly requires it, and provide explicit Cancel/Done behavior.
- Bind presentation to stable task state so one modal replaces another intentionally instead of stacking.
- Use WindowGroup and scene APIs for independent documents or durable tasks.
- In UIKit, select UIModalPresentationStyle and popover presentation from size and task; support adaptive presentation.
- Test dismissal by button, swipe, Escape, keyboard commands, and accessibility action.

## Decision Table

| Need | Presentation |
| --- | --- |
| Small nearby detail | Disclosure or popover |
| Short distinct task | Sheet |
| Supplementary controls affecting visible content | Inspector, side region, or nonmodal sheet |
| Complex focused editing | Full screen or dedicated window |
| Choices after an intentional risky action | Action sheet/confirmation dialog |
| Critical immediate problem | Alert |
| Independent document/task context | Window |

## Worked Example: Compose Message

The draft opens compose in a sheet, opens recipient search as a second sheet, opens attachment choice as a third, and alerts whenever the person tries to close.

Reconstruct it:

1. Use one compose sheet with a clear title, Send, and Cancel.
2. Keep recipient search inside the single task path or adapt it to an appropriate popover on wide iPad layouts.
3. Use a menu or system picker for attachments rather than stacking another sheet unnecessarily.
4. Autosave a draft. On dismissal, close directly when there is no meaningful content; otherwise use a confirmation dialog with Save Draft, Delete Draft, and Continue Editing.
5. On iPad, consider a dedicated compose window only when people benefit from keeping it beside mail content.

## Key Takeaways

- Choose the least disruptive presentation that protects task focus.
- Keep modal tasks short, single-path, and easy to dismiss.
- Present one modal or popover at a time.
- Use alerts only for critical, actionable interruptions and label outcomes precisely.
- Preserve work automatically when safe; use windows for durable parallel context.

## Connects To

- Chapter 11: Buttons, Menus, Toolbars, and Actions
- Chapter 12: Forms and Data Entry
- Chapter 16: Launch, Onboarding, Accounts, Settings, and Help
- Chapter 20: Design-to-Development Playbook

## Source Focus

Modality; Alerts; Sheets; Popovers; Action sheets; Windows; Going full screen; Navigation and search.
