The key requirement is:

P_PTI / PTI → dropdown → Yes / No
EPL Status → dropdown → Yes / No
If Yes, reveal its corresponding input field within Engine Details
If No, hide the dependent field
Both decision fields stay at the bottom of Engine Details
1. Overall Information Architecture
Vessel Management
│
└── Vessel List
      │
      ├── View Vessel
      ├── Edit Vessel
      └── Create Vessel
             │
             └── Create Vessel Information
                    │
                    ├── Vessel Details
                    │
                    ├── Engine Details
                    │      │
                    │      ├── Core Engine Fields
                    │      │
                    │      ├── PTI / P_PTI
                    │      │      └── If Yes → PTI Input
                    │      │
                    │      └── EPL Status
                    │             └── If Yes → EPL Input
                    │
                    └── Form Actions
                           ├── Vessel Creation via File
                           ├── Add / Edit Custom Fields
                           ├── Close
                           └── Submit
2. Create Vessel Information — Screen Architecture

The modal/page should have one clear hierarchy:

CREATE VESSEL INFORMATION
│
├── VESSEL DETAILS
│
│   ├── Company Name
│   ├── Vessel Name
│   ├── IMO Number
│   ├── Vessel Type
│   ├── Flag State
│   ├── Class Society
│   ├── GRT
│   ├── Port of Registry
│   └── Built Year
│
├── ENGINE DETAILS
│
│   ├── Existing Engine Fields
│   │
│   ├── PTI / P_PTI
│   │     ├── No → Nothing else shown
│   │     └── Yes → PTI Input Field
│   │
│   └── EPL Status
│         ├── No → Nothing else shown
│         └── Yes → EPL Input Field
│
└── ACTION FOOTER
      ├── Vessel Creation via File
      ├── Add / Edit Custom Fields
      ├── Close
      └── Submit
3. Section 1 — Vessel Details

The current top section should explicitly become:

VESSEL DETAILS

Use the existing 2-column grid.

┌─────────────────────────────────────────────────────────┐
│ VESSEL DETAILS                                          │
│                                                         │
│ Company Name              Vessel Name*                  │
│ [...................]     [.........................]   │
│                                                         │
│ IMO Number*               Vessel Type*                  │
│ [...................]     [.........................]   │
│                                                         │
│ Flag State*               Class Society*               │
│ [...................]     [.........................]   │
│                                                         │
│ GRT*                      Port of Registry*             │
│ [...................]     [.........................]   │
│                                                         │
│ Built Year*                                             │
│ [...................................................]    │
└─────────────────────────────────────────────────────────┘

Do not change the existing input visual style.

4. Section 2 — Engine Details

After Vessel Details:

────────────────────────────────────────────────────────

ENGINE DETAILS

All engine-related information remains here.

The existing engine fields should remain in their current structure.

Then, at the bottom of this section, place the two decision fields.

5. PTI / P_PTI Architecture

The field should be a dropdown, not radio buttons.

Default
PTI (P_PTI)*
[ Select Yes / No ▼ ]

Options:

Select
Yes
No
If user selects No

Nothing else appears.

PTI (P_PTI)*
[ No ▼ ]

The form stays compact.

If user selects Yes

Reveal the dependent input immediately below it:

PTI (P_PTI)*
[ Yes ▼ ]

PTI Details*
[................................................]

The new input should feel visually connected to PTI.

Do not move it somewhere else in the form.

6. EPL Status Architecture

Same pattern.

Default
EPL Status*
[ Select Yes / No ▼ ]

Options:

Select
Yes
No
If No
EPL Status*
[ No ▼ ]

Nothing else appears.

If Yes
EPL Status*
[ Yes ▼ ]

EPL Details*
[................................................]

Again, the conditional input appears directly below the field that controls it.

7. Final Engine Details Layout

This is the important part.

Default state
ENGINE DETAILS
────────────────────────────────────────────────────────

Engine Field 1*             Engine Field 2*
[...................]       [...................]

Engine Field 3*             Engine Field 4*
[...................]       [...................]

Engine Field 5*             Engine Field 6*
[...................]       [...................]

PTI (P_PTI)*
[ Select Yes / No ▼ ]

EPL Status*
[ Select Yes / No ▼ ]

This keeps PTI and EPL at the bottom.

8. PTI = Yes State
ENGINE DETAILS
────────────────────────────────────────────────────────

Engine fields...

PTI (P_PTI)*
[ Yes ▼ ]

PTI Details*
[................................................]

EPL Status*
[ Select Yes / No ▼ ]

The PTI input appears between PTI and EPL.

9. Both = Yes State
ENGINE DETAILS
────────────────────────────────────────────────────────

Engine fields...

PTI (P_PTI)*
[ Yes ▼ ]

PTI Details*
[................................................]

EPL Status*
[ Yes ▼ ]

EPL Details*
[................................................]

This is the cleanest state because the dependency is immediately understandable.

10. Why Dropdown Instead of Radio

Since you specifically want dropdowns, document this as a deliberate requirement.

Use MUI Select
PTI (P_PTI)*
[ Select ▼ ]

Options:

Select
Yes
No

Same for:

EPL Status*
[ Select ▼ ]

This also saves horizontal space inside the two-column form.

11. Conditional Logic

The MD should explicitly define this behavior.

P_PTI
│
├── Select
│     └── No dependent field
│
├── No
│     └── No dependent field
│
└── Yes
      └── Show PTI Details input

And:

EPL Status
│
├── Select
│     └── No dependent field
│
├── No
│     └── No dependent field
│
└── Yes
      └── Show EPL Details input
Important behavior

If the user changes:

Yes → No

the dependent input should disappear.

If the user changes:

No → Yes

the dependent input should appear again.

If the user changes Yes → No after entering a value, the implementation should clear the dependent value or explicitly preserve it according to the product's data rule. For the first implementation, I recommend clearing it to avoid submitting stale conditional data.

12. Visual Behavior of Conditional Fields

Don't make the field suddenly appear with a dramatic animation.

Use a subtle layout expansion.

Example:

PTI (P_PTI)*
[ Yes ▼ ]

PTI Details*
[................................]

The new field should use exactly the same input component as the rest of the form.

No:

New card
Colored container
New background
Modal
Accordion
Tooltip
Badge
Heavy animation

The relationship itself should communicate the dependency.

13. Footer Architecture

The existing footer should remain fixed at the bottom.

┌─────────────────────────────────────────────────────────────┐
│                                                             │
│ [Vessel Creation via File] [Add / Edit Custom fields]       │
│                                                             │
│                              [Close] [Submit]               │
└─────────────────────────────────────────────────────────────┘

Do not move these actions into the Engine Details section.

14. Complete Screen Blueprint
┌───────────────────────────────────────────────────────────────┐
│                                                               │
│                 CREATE VESSEL INFORMATION                     │
│                                                               │
│ ┌───────────────────────────────────────────────────────────┐ │
│ │                                                           │ │
│ │ VESSEL DETAILS                                            │ │
│ │ ───────────────────────────────────────────────────────── │ │
│ │                                                           │ │
│ │ Company Name                 Vessel Name*                 │ │
│ │ [....................]       [.........................]  │ │
│ │                                                           │ │
│ │ IMO Number*                  Vessel Type*                 │ │
│ │ [....................]       [.........................]  │ │
│ │                                                           │ │
│ │ Flag State*                  Class Society*               │ │
│ │ [....................]       [.........................]  │ │
│ │                                                           │ │
│ │ GRT*                         Port of Registry*             │ │
│ │ [....................]       [.........................]  │ │
│ │                                                           │ │
│ │ Built Year*                                                │ │
│ │ [.......................................................]  │ │
│ │                                                           │ │
│ │ ───────────────────────────────────────────────────────── │ │
│ │                                                           │ │
│ │ ENGINE DETAILS                                             │ │
│ │ ───────────────────────────────────────────────────────── │ │
│ │                                                           │ │
│ │ Engine Field*                 Engine Field*               │ │
│ │ [....................]        [.........................] │ │
│ │                                                           │ │
│ │ Engine Field*                 Engine Field*               │ │
│ │ [....................]        [.........................] │ │
│ │                                                           │ │
│ │ Engine Field*                 Engine Field*               │ │
│ │ [....................]        [.........................] │ │
│ │                                                           │ │
│ │ PTI (P_PTI)*                                             │ │
│ │ [ Select Yes / No ▼ ]                                    │ │
│ │                                                           │ │
│ │ EPL Status*                                               │ │
│ │ [ Select Yes / No ▼ ]                                    │ │
│ │                                                           │ │
│ └───────────────────────────────────────────────────────────┘ │
│                                                               │
├───────────────────────────────────────────────────────────────┤
│ [Vessel Creation via File] [Add / Edit Custom fields]        │
│                                      [Close]       [Submit]   │
└───────────────────────────────────────────────────────────────┘
15. With PTI = Yes
PTI (P_PTI)*
[ Yes ▼ ]

PTI Details*
[................................................]
16. With EPL = Yes
EPL Status*
[ Yes ▼ ]

EPL Details*
[................................................]
17. With Both = Yes
PTI (P_PTI)*
[ Yes ▼ ]

PTI Details*
[................................................]

EPL Status*
[ Yes ▼ ]

EPL Details*
[................................................]
18. IA Summary for the MD

I would put this at the beginning of your MD file:

Create Vessel Information
│
├── Vessel Details
│   ├── Company Name
│   ├── Vessel Name
│   ├── IMO Number
│   ├── Vessel Type
│   ├── Flag State
│   ├── Class Society
│   ├── GRT
│   ├── Port of Registry
│   └── Built Year
│
├── Engine Details
│   ├── Existing Engine Fields
│   │
│   ├── PTI (P_PTI)
│   │   ├── Yes
│   │   │   └── PTI Details
│   │   └── No
│   │
│   └── EPL Status
│       ├── Yes
│       │   └── EPL Details
│       └── No
│
└── Actions
    ├── Vessel Creation via File
    ├── Add / Edit Custom Fields
    ├── Close
    └── Submit
Core design principle

PTI and EPL are decision fields, not ordinary engine fields.

Therefore:

Decision → immediate dependent field → continue form

rather than:

Decision → jump somewhere → new field appears → user wonders why.

That should be the central UX rule in the MD. Once you add the actual names/types of the PTI Details and EPL Details input fields, the MD will be ready for the implementation prompt.