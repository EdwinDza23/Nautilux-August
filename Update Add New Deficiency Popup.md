Update Add New Deficiency Popup

Update the Add New Deficiency popup in the PSC List module.

1. Primary reference — do not redesign

The existing/old Nautilux application popup is the source of truth for the visual design.

Use the screenshots/images I provided and the assets inside:

asset/psc list/

Also use:

The existing popupvideo reference for popup behavior/layout.
The expand folder assets for the expanded textarea/modal behavior.
The provided DevTools screenshots/code measurements where useful.

Do not invent a new modal design. Reproduce the existing Nautilux popup style.

The final result at 100% browser zoom should visually look like the existing application popup.

2. Popup dimensions & structure

Match the existing popup's:

Width
Height
Header height
Footer height
Internal spacing
Border radius
Position
Scroll behavior
Field sizing
Typography
Colors
Shadows
Overlay opacity

The popup is intentionally long vertically, so:

Keep the popup at the established application size.
Do NOT shrink the content to fit everything.
Use a vertical scrollbar inside the popup.
Header remains fixed.
Footer remains fixed.
Only the content area scrolls.

Structure:

┌─────────────────────────────────────────────┐
│ Add New Deficiency                     X    │ ← fixed header
├─────────────────────────────────────────────┤
│                                             │
│ Scrollable form content                     │
│                                             │
│ ...                                         │
│ ...                                         │
│                                             │
├─────────────────────────────────────────────┤
│                         Cancel      Save     │ ← fixed footer
└─────────────────────────────────────────────┘
3. Visual styling

Match the existing Nautilux application exactly.

Header

Use the existing:

Gold/mustard header background
Dark text
Same typography
Same font weight
Same padding
Same X close icon
Same icon size and positioning

Header title:

Add New Deficiency

Do not change the wording.

Footer

Use the existing gold/mustard footer.

Buttons:

Cancel
Save

Match the old application's:

Button dimensions
Dark background
White text
Border radius
Padding
Position
Spacing
4. Form fields

Keep every existing field and the exact existing order.

Do NOT remove, rename, reorder, or invent fields.

The order must remain:

Deficiency Code *
Deficiency Area *
Summary
Training Courses
Deficiency Description
Action Code *
Action Code Desc
Corrective Action
Below are the comments provided by the reviewer
Risk Assessment checkbox
Solaristech Corrective Action Plan checkbox
Suggested
Risk Assessment
Solaristech Corrective Action Plan

Use the existing application's input components/styles.

5. Input styling

All fields must use the same input/dropdown/text-area component style already used across Nautilux.

Match:

Floating labels
Border
Border thickness
Border radius
Background
Font
Font size
Label size
Label positioning
Placeholder behavior
Focus state
Disabled state
Dropdown arrow
Internal padding
Vertical spacing

Do not create a separate visual language for this popup.

6. Existing data flow

Preserve the existing functionality.

Deficiency Code

When the user selects a Deficiency Code:

Immediately populate:

Deficiency Area
Summary
Training Courses
Deficiency Description

Use a subtle light loading animation while the dependent data is being populated.

Field editability
Field	Behavior
Deficiency Code	Editable / selectable
Deficiency Area	Read-only
Summary	Editable
Training Courses	Read-only
Deficiency Description	Editable
Action Code	Editable / selectable
Action Code Desc	Auto-populated
Corrective Action	Editable
Suggested	AI-generated/mock data
Risk Assessment	AI-generated/mock data
Solaristech Corrective Action Plan	AI-generated/mock data

Do not change this behavior.

7. Action Code behavior

When the user selects:

Action Code

automatically populate:

Action Code Desc

with the corresponding mock data.

Do not require the user to manually enter Action Code Desc.

8. Generate Recommendation

Add a button called:

Generate Recommendation

Place it in a safe, obvious and user-friendly location next to the Action Code Desc / Corrective Action area, without disturbing the established form hierarchy.

The button should visually fit the existing Nautilux application.

Prefer the existing primary dark-green button style.

Do not make it visually overpower the Save button.

Example:

Action Code *                 [▼]


Action Code Desc              [Generate Recommendation]
────────────────────────────────────────────────────────


Corrective Action
┌──────────────────────────────────────────────────────┐
│                                                      │
└──────────────────────────────────────────────────────┘

Use a sensible responsive arrangement if the available width becomes smaller.

9. AI recommendation behavior

For now, this is mock functionality only.

When the user clicks:

Generate Recommendation

show a short loading state, then populate all three fields:

Suggested

Populate mock recommendation data.

Risk Assessment

Populate mock risk assessment data.

Solaristech Corrective Action Plan

Populate mock corrective action plan data.

The three fields should be populated together.

Use a subtle loading animation consistent with Nautilux.

Do not implement a real AI/API integration.

Keep the code structured so the mock implementation can later be replaced by an API call.

10. Expand functionality

For multiline fields that have the existing expand icon, preserve the expand icon and behavior.

Use the assets/reference from:

asset/psc list/expand/

The fields requiring expand functionality should include:

Deficiency Description
Corrective Action
Suggested
Risk Assessment
Solaristech Corrective Action Plan

When the user clicks the expand icon:

Open the expanded view/modal.
Match the provided Risk Assessment expanded reference.
Use the same Nautilux visual language.
Keep the field content synchronized with the main popup.
Allow the user to close the expanded view.
Do not lose or reset entered/generated content.

The expanded view should have:

Same header treatment
Field title
Large readable content area
Internal vertical scrolling
Close button
Same Nautilux colors
Same typography
Same spacing
Same border/shadow treatment
11. Save button logic

The Save button must remain disabled until:

Action Code has been selected.

Before Action Code selection:

Save → Disabled

After Action Code selection:

Save → Enabled

Do not enable Save merely because Deficiency Code has been selected.

Preserve any other existing validation logic.

12. Scroll behavior

This is important.

The popup is a long form.

Implement:

Popup
 ├── Fixed Header
 ├── Scrollable Content
 └── Fixed Footer

The scrollbar must belong to the popup content area—not the entire page.

When scrolling:

Header stays visible.
Footer stays visible.
Form content scrolls vertically.
No horizontal overflow.
No content should be hidden underneath the footer.
13. 100% viewport fidelity

At 100% browser zoom, compare the implementation against the supplied screenshots.

Pay special attention to:

Popup width
Popup height
Header height
Footer height
Field widths
Field heights
Vertical gaps
Horizontal padding
Scrollbar position
Button dimensions
Typography
Expand icons
Close icon

Do not simply approximate the reference.

14. Existing Nautilux design system

Do NOT introduce:

New colors
New fonts
New border styles
New button styles
New modal styles
Glassmorphism
Excessive shadows
Gradients
AI-looking UI
Generic modern SaaS modal patterns

The popup should look like it belongs to the existing Nautilux application.

Reuse existing CSS/classes/components wherever possible.

If an existing Nautilux input/dropdown/modal component already exists, reuse it instead of creating another version.

15. Important implementation rule

Before modifying anything:

Inspect the current Add New Deficiency implementation.
Identify existing components/classes/styles.
Identify the current data relationships between:
Deficiency Code
Deficiency Area
Summary
Training Courses
Deficiency Description
Action Code
Action Code Desc
Identify the existing popup/modal implementation.
Identify existing expand functionality if present.
Reuse existing components wherever possible.
Only modify what is necessary.

Do not break the existing PSC List flow.