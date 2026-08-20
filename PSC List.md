1. Core User Journey
PSC List
   │
   │ Click "Create"
   ▼
Vessel Details
   │
   │ Select Vessel
   ▼
Auto-populate Vessel Information
   │
   │ Select PSC Details
   │
   │ Type
   │ Sub Type
   │ Country
   │ Port of Detection
   │ Date
   │ PSC Region
   ▼
"Add PSC" becomes enabled
   │
   │ Click Add PSC
   ▼
Add New Deficiency Modal
   │
   │ Enter deficiency information
   │
   │ Deficiency Code
   │ Deficiency Area
   │ Summary
   │ Training Courses
   │ Description
   │ Action Code
   │ Action Code Description
   │ Corrective Action
   ▼
Save
   │
   ▼
PSC Record Created
   │
   ▼
PSC List
   │
   └── New record appears with status
2. Detailed User Journey
Step 1 — PSC List

User lands on PSC LIST.

Existing functionality:

Search
Status filter
Company filter
From Date
To Date
Create
PSC records table
Expand/collapse row

Primary action:

Create

Step 2 — Vessel Details

Clicking Create opens the Vessel Details screen.

Initially:

VESSEL NAME *
IMO NUMBER
DOC COMPANY
FLAG STATE


CLASS SOCIETY
VESSEL TYPE
GROSS TONNAGE
PORT OF REGISTRY

Only Vessel Name is user-selectable.

Vessel selection

User opens:

VESSEL NAME *

Dropdown/searchable input.

Example:

ABCD
ABCD
AB SERENA
ACADIA
AMBER ECO
AMI VESSEL -1
AQUAA ECO
...

Once a vessel is selected:

VESSEL NAME → ABCD


IMO NUMBER       → 88
DOC COMPANY      → DENALI
FLAG STATE       → Argentina
CLASS SOCIETY    → ABS
VESSEL TYPE      → Anchor Handling Tug Supply
GROSS TONNAGE    → 12
PORT OF REGISTRY → Buenos Aires
Important behavior

These fields should be automatically populated from the selected vessel.

The user should not manually enter or modify these vessel master-data fields in this flow unless the existing application explicitly allows editing.

3. PSC Details

After vessel selection, user moves to:

PSC DETAILS
TYPE *
SUB TYPE *
COUNTRY *
PORT OF DETECTION *


DATE *
PSC REGION *

Dropdown options observed from the screenshots:

Type
PSC
Sub Type
POST DETENTION
DEFICIENCY
Port of Detection

Example:

Durres
Shengjin
Vlores
PSC Region

Example options visible:

Paris MoU
Tokyo MoU
USCG
Vina del Mar
Caribbean MoU
...
Date

Native/custom date picker.

Format:

dd-mm-yyyy
4. Form State / Button Logic

This is important for development.

Initial state
Vessel:          Empty
Type:            Empty
Sub Type:        Empty
Country:         Empty
Port:            Empty
Date:            Empty
PSC Region:      Empty


Add PSC:         DISABLED
After vessel selection
Vessel fields:   Auto-populated


PSC fields:      Empty


Add PSC:         DISABLED
After incomplete PSC details

Still:

Add PSC: DISABLED
After all required PSC fields are valid
Vessel ✓
Type ✓
Sub Type ✓
Country ✓
Port ✓
Date ✓
PSC Region ✓


Add PSC: ENABLED
5. Add New Deficiency

Clicking Add PSC opens:

Add New Deficiency

This should behave as a focused modal over the Vessel Details page.

Background:

Darkened overlay
Vessel Details remains visible behind it
Modal has its own vertical scroll
Header remains visible
Footer remains visible
Header
Add New Deficiency                         X
Form
Deficiency Code *
[ Select ▼ ]


Deficiency Area *
[ Input ]


Summary
[ Textarea ]


Training Courses
[ Select ▼ ]


Deficiency Description
[ Textarea ]


Action Code *
[ Select ▼ ]   [ Eye ]


Action Code Desc
[ Textarea ]


Corrective Action
[ Textarea ]

Footer:

[ Cancel ]    [ Save ]
6. Deficiency Form State
Initial state
Deficiency Code     Empty
Deficiency Area     Empty
Summary             Empty
Training Courses    -
Description         Empty
Action Code         Empty
Action Code Desc    Empty
Corrective Action   Empty


Save → Disabled
Required fields

From the UI, at minimum:

Deficiency Code *
Deficiency Area *
Action Code *

You should confirm whether other fields are required by the backend/business rules.

Valid state

Once required fields are completed:

Save → Enabled
7. Save Behaviour

On Save:

Validate form
      ↓
Valid?
 ┌────┴────┐
 No        Yes
 ↓          ↓
Show       Create
errors     deficiency
             ↓
       Attach to PSC record
             ↓
       Close modal

The user should then be able to see the newly added deficiency associated with the PSC record.

8. Important: Multiple Deficiencies

I would design this workflow to support multiple deficiencies under one PSC inspection.

Conceptually:

PSC Inspection
│
├── Vessel
├── PSC Details
│
└── Deficiencies
    ├── Deficiency 1
    ├── Deficiency 2
    ├── Deficiency 3
    └── ...

So after saving one deficiency, the user should be able to add another rather than creating another PSC inspection.

Recommended flow:

PSC Details
     ↓
Add PSC
     ↓
Add New Deficiency
     ↓
Save
     ↓
Deficiency added
     ↓
[ + Add Deficiency ]
     ↓
Add another if required

This is the cleaner domain model.

9. Recommended State Model

For development, think of the module as these states:

STATE 01
PSC_LIST


        ↓ Create


STATE 02
VESSEL_SELECTION


        ↓ Vessel selected


STATE 03
VESSEL_DETAILS_POPULATED


        ↓ Complete PSC details


STATE 04
PSC_FORM_READY


        ↓ Add PSC


STATE 05
DEFICIENCY_MODAL


        ↓ Save


STATE 06
DEFICIENCY_ADDED


        ↓ Add another / finish


STATE 07
PSC_RECORD_CREATED
10. Error / Validation Flow

The implementation should also account for:

Vessel not selected
Vessel Name is required
Required PSC field missing
Please select [field]
Invalid date

Prevent invalid date submission.

Deficiency required field missing

Show validation directly beside the relevant field.

Save failure

Keep the modal open and show an error message.

Do not clear entered data after an error.

11. Navigation Model

I would keep the navigation simple:

PSC List
   │
   └── Create
        │
        ▼
   Vessel Details
        │
        ├── Back → PSC List
        │
        └── Add PSC
              │
              ▼
        Add New Deficiency
              │
              ├── Cancel → Vessel Details
              │
              └── Save → Vessel Details

The X on the modal should behave the same as Cancel.

12. UI Component Structure

For implementation, I would break it into reusable components:

PSCModule
│
├── PSCList
│   ├── SearchBar
│   ├── Filters
│   ├── PSCDataTable
│   └── ExpandablePSCRow
│
├── CreatePSC
│   ├── PageHeader
│   ├── VesselDetailsSection
│   │   └── VesselSelect
│   │
│   ├── PSCDetailsSection
│   │   ├── TypeSelect
│   │   ├── SubTypeSelect
│   │   ├── CountrySelect
│   │   ├── PortSelect
│   │   ├── DatePicker
│   │   └── PSCRegionSelect
│   │
│   └── AddPSCButton
│
└── AddDeficiencyModal
    ├── DeficiencyCodeSelect
    ├── DeficiencyAreaInput
    ├── SummaryTextarea
    ├── TrainingCourseSelect
    ├── DescriptionTextarea
    ├── ActionCodeSelect
    ├── ActionCodeDescription
    ├── CorrectiveAction
    └── ModalFooter
13. Data Relationship

The underlying structure should ideally be:

Company
   │
   └── Vessel
         │
         └── PSC Inspection
               │
               ├── Type
               ├── Sub Type
               ├── Country
               ├── Port
               ├── Date
               ├── PSC Region
               │
               └── Deficiencies[]
                     │
                     ├── Code
                     ├── Area
                     ├── Summary
                     ├── Training
                     ├── Description
                     ├── Action Code
                     ├── Action Description
                     └── Corrective Action

This is much better than treating each deficiency as a separate PSC record.

14. UX Rules I Would Carry Into Development
Auto-populate aggressively: vessel master data should never be re-entered.
Progressive disclosure: don't show the deficiency modal until PSC details are complete.
Clear required fields: use the existing * convention consistently.
Preserve user input: validation errors must not reset the form.
Reusable Nautilux controls: dropdowns, date picker, text fields, buttons, modal and spacing should match the existing application.
Modal scroll: only the modal body should scroll; header/footer remain stable.
Keyboard accessibility: dropdowns, modal close, Cancel and Save should be keyboard accessible.
Avoid unnecessary confirmation dialogs: Save → add deficiency directly.
Support multiple deficiencies: one PSC inspection can contain multiple deficiencies.
15. One-Line Product Flow

PSC List → Create → Select Vessel → Auto-populate Vessel Details → Complete PSC Details → Add PSC → Add Deficiency → Save → Add More Deficiencies or Finish → PSC Record appears in PSC List.