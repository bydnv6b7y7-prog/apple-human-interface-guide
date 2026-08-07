# Chapter 12: Forms, Selection, and Data Entry

## Core Idea

A form should ask for the least information, in the easiest available format, at the moment it is needed. Prefer system data, strong defaults, choices, and direct manipulation over typing. Match each control to the structure of the value and validate without discarding work.

## Frameworks Introduced

### Input-effort order

Prefer, from lowest effort to highest:

1. Derive or retrieve with permission.
2. Prefill a safe default.
3. Select from visible choices.
4. Adjust a constrained control.
5. Paste, drag, scan, or dictate.
6. Type free-form content.

### Control-to-value mapping

- **Toggle:** Binary on/off state.
- **Toggle button:** Binary state outside a settings/list row.
- **Segmented control:** Small set of closely related views or states.
- **Picker:** Predictable ordered set of choices.
- **Menu:** Short set of commands or values depending on configuration.
- **Slider:** Continuous range where relative position matters.
- **Stepper:** Small incremental changes.
- **Text field:** One line or a small amount of text.
- **Text editor/view:** Long or multiline text.
- **Secure field:** Sensitive secret entry.
- **DatePicker:** Date or time components.

## Key Concepts

### Ask only what the task needs

Remove fields that are merely useful to the business but unnecessary for the person’s outcome. Postpone profile completion and preferences. If the system already holds an address, contact, payment method, password, or date in a privacy-respecting form, offer the platform mechanism rather than making the person retype it.

### Use defaults without creating surprise

Prefill common, low-risk values and make them easy to inspect. Never silently preselect an expensive add-on, privacy-sensitive option, or irreversible choice. A default should save work, not manufacture consent.

### Keep labels visible

Place persistent labels near fields. Placeholder text can show an example or format but cannot carry the only label because it disappears during entry. Use a hint only when the expected value is not obvious.

Match keyboard and content metadata to the field:

- Email, phone, URL, number, decimal, and other appropriate keyboard types.
- Text content types for AutoFill.
- Submit labels such as Next, Search, Send, or Done.
- Capitalization, correction, and secure-entry behavior appropriate to the content.

Never prepopulate a password field. Use password AutoFill, passkeys, and system authentication where possible.

### Validate as the person can act

Validate format when enough input exists and present an inline, actionable correction. Preserve the entered text. Do not show an error before the person has had a reasonable chance to complete the field.

Keep Continue or the result action available once required information is present. For server-side checks, communicate progress and keep the form recoverable.

### Choose selection controls by set size and semantics

Use a toggle only for a true binary state, not to perform a one-time command. On iOS, a switch works naturally in a list row; outside a list, a toggle-style button can better preserve context. Its state needs more than color.

Use a segmented control for a few closely related states or views. Keep labels short and consistent; do not mix text and symbols in one control or mix actions with selection. Source guidance suggests up to about five segments on iPhone, with five to seven possible in wider contexts. Use a tab bar for independent app sections.

Use a picker for a medium or long predictable ordered set. A short flat set may fit a menu; a very large searchable collection may need a list or dedicated selection page.

### Match range controls to precision

Use a slider when relative continuous adjustment is meaningful. Add labels or endpoints, update the result live, and provide a text field or stepper if exact input matters. Prefer horizontal sliders. Do not create an app slider for system volume; use the system control.

Use a stepper for small discrete increments. Pair it with visible current value and allow direct numeric entry when large changes are likely.

### Keep forms responsive to the keyboard

The focused field, validation, and next action must remain visible. Scroll rather than shift the entire page by a fixed offset. Use the keyboard layout guide or safe-area behavior and support hardware keyboards without leaving artificial empty space.

## Mental Models

### Value shape

Identify the data shape before selecting a component:

- Boolean → toggle.
- Small exclusive set → segmented control.
- Ordered known set → picker.
- Continuous range → slider.
- Incremental number → stepper.
- Open text → field/editor.

### Completion path

Trace the fastest valid path from first field to result. Optimize focus order, keyboard type, Next/Done behavior, defaults, and validation for that path while preserving alternatives.

### Cost of an error

Use lighter validation for easily corrected, reversible fields. Add stronger review or confirmation only when incorrect input creates meaningful financial, privacy, safety, or irreversible consequences.

## Anti-patterns

- Asking for data available through an appropriate system capability.
- Placeholder-only labels.
- One generic keyboard for every field.
- A switch that performs “Send,” “Delete,” or another action.
- Segmented controls with too many items, mixed symbols and text, or unrelated destinations.
- A slider for an exact value without a precise alternative.
- Clearing the entire form after one validation or network error.
- Disabling Continue with no visible explanation.
- Validating an empty field as an error before interaction.
- Fixed keyboard offsets that break on iPad or hardware keyboard use.

## Implementation Bridge

- Use Form, Section, TextField, SecureField, TextEditor, Toggle, Picker, Slider, Stepper, and DatePicker for semantic behavior.
- Configure keyboard type, text content type, submit label, focus order, and AutoFill.
- Use FocusState to move through fields intentionally; do not automatically focus on iPad when opening the software keyboard harms context.
- Keep validation state in the form model and expose errors through text plus accessibility announcements.
- Use the keyboard layout guide in UIKit or safe-area-aware scrolling in SwiftUI.
- Persist drafts when leaving or when remote submission fails.

## Decision Table

| Data | Preferred input | Escalate when |
| --- | --- | --- |
| Agree to setting | Toggle | It is actually an action or consent event |
| 2–5 related modes | Segmented control | Labels do not fit or sections are independent |
| Country or category | Picker/searchable list | The set is very large |
| Brightness-like range | Slider | Exact numeric value matters |
| Quantity 1–10 | Stepper | Large jumps are common |
| Email | Text field with email metadata | System account selection can remove entry |
| Password | Secure field with AutoFill/passkey path | Avoid custom credential flow |
| Notes | Text editor | Rich document editing needs a dedicated experience |

## Worked Example: Checkout Address

The draft asks for full name, country, state, city, postal code, address, phone, delivery notes, account password, and marketing opt-in in one rigid form.

Reconstruct it:

1. Offer system contact/address AutoFill and prefill known account data with permission.
2. Ask only for fields required by the selected country and delivery method.
3. Use persistent labels, correct content types, locale-aware formatting, and Next/Done focus progression.
4. Validate postal code and phone only after enough input exists; explain the exact correction.
5. Put optional delivery notes behind a clear optional field or disclosure.
6. Keep marketing choice separate, unselected, and clearly described; do not bundle it with transaction consent.
7. Do not ask for the account password if system authentication or an existing session can authorize payment.
8. Preserve the form and show local recovery if address verification fails.

## Key Takeaways

- Minimize entry and prefer system data, defaults, choices, and direct manipulation.
- Select controls from the value’s shape and the size of its choice set.
- Keep labels visible and configure keyboard and AutoFill metadata.
- Validate locally, actionably, and without losing work.
- Design the full completion path, including keyboard and failure states.

## Connects To

- Chapter 5: Typography and Writing
- Chapter 7: Accessibility, Privacy, and Localization
- Chapter 11: Buttons, Menus, Toolbars, and Actions
- Chapter 13: Modality and Presentation

## Source Focus

Entering data; Text fields; Text views; Pickers; Toggles; Segmented controls; Sliders; Steppers; Virtual keyboards; Forms; Managing accounts.
