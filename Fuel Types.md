Fuel Configuration --- Fuel Types Screen

Purpose

Implement the Fuel Types screen under Maintenance → Fuel
Configuration.

This screen must preserve the existing product UI exactly. Do not
redesign the page, introduce a new visual style, or modernize existing
components.

The implementation must use MUI (Material UI).

Reference Assets

The Fuel Types screenshots have been added to the project's asset
folder and must be used as the visual source of truth.

Reference screenshots:

a2ef242b-e213-4e1a-9e4c-5d4edf3d2546.png --- Fuel Types screen

1efd1d30-8dd4-4dfd-a317-90e3262f0d3d.png --- Add Fuel Details
modal

Use these screenshots to match: - Overall layout - Colors - Typography -
Spacing - Table proportions - Input dimensions - Button styling - Border
radius - Shadows - Icons - Modal dimensions - Alignment

Navigation Change

Current sidebar item:

Fuel

Change the displayed name to:

Fuel Configuration

Keep the existing sidebar icon, active-state styling, position, spacing,
and interaction unchanged.

Do not change the rest of the sidebar.

Page Structure

The Fuel Configuration page contains two selectable views:

Fuel Types

EUA Price

The selector is positioned at the right side of the page header,
matching the existing page hierarchy.

For the Fuel Types screen:

Fuel Types is selected.

EUA Price is unselected.

Use a simple MUI radio/selection control consistent with the existing
product styling. Do not introduce a large modern tab component or
pill-style navigation.

Switching to EUA Price should replace the content area without
navigating away from Fuel Configuration.

Fuel Types Screen

Page Header

Title:

FUEL TYPES

Supporting text:

Manage and update fuel types and their associated emission metrics. These values are used across vessels for rating and reporting.

Keep the title and description placement, typography, spacing, and color
consistent with the reference screenshot.

Search and Action Area

Place the search and actions exactly as shown in the reference.

Structure:

[ Search ] [ Search ] [ + ADD FUEL TYPE ]

Search Input

MUI input/text field

Same width and height as the reference

Same beige background

Same border

Same radius

Same typography

Placeholder: Search

Search Button

Label:

Search

Keep the existing dark green button style.

Do not replace it with an icon-only action.

Add Button

Label:

+ ADD FUEL TYPE

Use the same plus icon and button styling shown in the reference.

The button opens the existing Add Fuel Details modal.

Fuel Types Table

Use the same table structure and proportions shown in the screenshot.

Columns:

Column               Content

SLNO                 Sequential number
Fuel Type            Fuel name
Price per Ton ($)   Fuel price
Carbon               Carbon value
Action               Edit icon

Example data for the demo:

SLNO Fuel Type        Price per Ton (\$)       Carbon

   1 ADVN                           1900        82.02
   2 DAS                         23.3333         90.3
   3 DFHU                            650         8.74
   4 FUEL EU                        1200         0.39
   5 FUELSSSSSSSS              11111.111   11111.2222
   6 GAS                              99           89
   7 GFRT                             98         9.87
   8 HFO                             120          2.5

The values are demo/reference data only.

Table Styling

The table must visually match the screenshot.

Preserve:

Beige page background

Existing table header typography

Gold/yellow header text

Thin horizontal row separators

Existing row height

Existing column alignment

Existing left/right spacing

Existing action-column placement

Existing scrollbar behavior

Existing typography scale

Do not add: - Zebra striping - Rounded table cards - Extra borders -
Status badges - Sorting controls - Pagination redesign - New table
toolbar - Bulk selection - New action menus

unless already present in the existing implementation.

Action Icon

Use the same edit/pencil MUI icon shown in the reference.

The icon should remain:

Black

Small

Right aligned within the Action column

Vertically centered

Do not substitute a different icon.

Clicking the icon opens the Edit Fuel Details modal.

Add Fuel Details Modal

Clicking:

+ ADD FUEL TYPE

opens the existing modal style shown in the reference screenshot.

Modal title:

Add Fuel Details

Fields:

Fuel Type*

Price*

Carbon*

Buttons:

CANCEL

SAVE

Modal Visual Requirements

The modal must match the reference screenshot exactly in visual
language.

Preserve:

Centered modal

Existing width

Gold/yellow header

Beige body

Existing border radius

Existing shadow

Existing input height

Existing input border

Existing input spacing

Existing button positioning

Existing button sizes

Existing typography

Do not redesign the modal.

Edit Flow

Clicking the pencil icon opens the same modal in edit mode.

Title:

Edit Fuel Details

Pre-populate:

Fuel Type

Price

Carbon

Buttons remain:

CANCEL

SAVE

MUI Implementation

Use MUI components wherever possible.

Recommended components:

Box

Typography

TextField

Button

Radio

RadioGroup

FormControl

FormControlLabel

Table

TableContainer

TableHead

TableBody

TableRow

TableCell

Dialog

DialogTitle

DialogContent

DialogActions

IconButton

Use the existing project's MUI theme and tokens if available.

Do not create a separate visual design system for this screen.

Responsive Behavior

The existing desktop layout is the primary reference.

Maintain the existing behavior on smaller widths without changing the
visual language.

The table may scroll horizontally if required rather than compressing
columns excessively.

Non-Negotiable Design Constraint

100% visual consistency with the existing Fuel Types UI.

Do not: - Change the color palette - Change typography - Change spacing
system - Change button shape - Change table style - Change modal style -
Replace existing icons - Add gradients - Add glassmorphism - Add cards -
Add modern dashboard styling - Introduce unnecessary UX improvements

Only implement the required structural change:

Fuel → Fuel Configuration

and the new:

Fuel Types | EUA Price

selector.

The existing Fuel Types experience should otherwise remain visually
unchanged.

Expected Flow

Maintenance
    ↓
Fuel Configuration
    ↓
┌─────────────────────────────────────┐
│ Fuel Types              ○ EUA Price │
└─────────────────────────────────────┘
    ↓
Fuel Types selected
    ↓
Fuel Types table
    ↓
+ ADD FUEL TYPE
    ↓
Add Fuel Details modal
    ↓
SAVE
    ↓
Fuel Types table updated

Edit flow:

Fuel Types table
    ↓
Click pencil icon
    ↓
Edit Fuel Details
    ↓
Update values
    ↓
SAVE
    ↓
Fuel Types table updated

Implementation Priority

Match the reference screenshot.

Preserve existing MUI components/styles.

Add Fuel Configuration naming.

Add Fuel Types / EUA Price selector.

Keep Fuel Types behavior unchanged.

Ensure Add/Edit modal matches the reference.

Avoid all unnecessary UI changes.