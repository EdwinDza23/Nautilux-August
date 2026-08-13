Maintenance → Fuel Configuration

Inside Fuel Configuration, the right side has exactly two radio/segmented options:

● Fuel Types  ○ EUA Price

Clicking EUA Price swaps the content area to the EUA pricing table.

I could not retrieve the Sidebar.md content from the uploaded-file search, so the blueprint below is based on the sidebar screenshot you provided and the confirmed requirements.

1. User Flowchart
┌──────────────────────┐
│      CLIENT PORTAL   │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│     Maintenance      │
│       Expanded       │
└──────────┬───────────┘
           │
           ▼
┌─────────────────────────────┐
│     Fuel Configuration      │
│     Sidebar navigation      │
└─────────────┬───────────────┘
              │
              ▼
┌─────────────────────────────────────────┐
│          FUEL CONFIGURATION             │
│                                         │
│  Left: Page title                       │
│  Right:                                 │
│  ● Fuel Types     ○ EUA Price           │
└──────────────┬──────────────────────────┘
               │
       ┌───────┴────────┐
       │                │
       ▼                ▼
┌───────────────┐  ┌────────────────┐
│  FUEL TYPES   │  │    EUA PRICE   │
└───────┬───────┘  └───────┬────────┘
        │                   │
        ▼                   ▼
┌─────────────────┐  ┌────────────────────┐
│ Existing Fuel   │  │ EUA Price Table    │
│ Types Table     │  │                    │
│                 │  │ Year               │
│ Fuel Type       │  │ VCM Price Min      │
│ Price / Ton     │  │ VCM Price Max      │
│ Carbon          │  │ EUA Price          │
│ Action          │  │ Action             │
└───────┬─────────┘  └─────────┬──────────┘
        │                      │
        ▼                      ▼
┌─────────────────┐    ┌──────────────────┐
│ Edit / Add Fuel │    │ + ADD EUA PRICE  │
│     Modal       │    └────────┬─────────┘
└─────────────────┘             │
                                ▼
                       ┌──────────────────┐
                       │ Add EUA Price    │
                       │     Modal        │
                       │                  │
                       │ Year             │
                       │ VCM Price Min    │
                       │ VCM Price Max    │
                       │ EUA Price        │
                       │                  │
                       │ CANCEL   SAVE    │
                       └────────┬─────────┘
                                │
                                ▼
                       ┌──────────────────┐
                       │ Updated EUA      │
                       │ Price Table      │
                       └──────────────────┘
2. Navigation Blueprint
Current
Maintenance
├── Company Details
├── Vessel List
├── User List
└── Fuel
New
Maintenance
├── Company Details
├── Vessel List
├── User List
└── Fuel Configuration

Important: Only rename Fuel → Fuel Configuration. Do not change the visual treatment of the sidebar.

3. Fuel Configuration — Page Blueprint

Keep the existing page almost pixel-for-pixel.

┌──────────────────────────────────────────────────────────────────────┐
│                                                                      │
│  FUEL CONFIGURATION                         ● Fuel Types  ○ EUA Price │
│  Manage and update fuel configuration.                              │
│                                                                      │
│  ┌──────────────────────────────────────────┐ ┌────────┐ ┌──────────┐│
│  │ Search                                   │ │ Search │ │ + ADD... ││
│  └──────────────────────────────────────────┘ └────────┘ └──────────┘│
│                                                                      │
│  ─────────────────────────────────────────────────────────────────── │
│                                                                      │
│  SLNO      Fuel Type          Price per Ton ($)       Carbon   Action│
│                                                                      │
│  1         ADVN               1900                    82.02      ✎   │
│  2         DAS                23.3333                 90.3       ✎   │
│  3         DFHU               650                     8.74       ✎   │
│  4         FUEL EU            1200                    0.39       ✎   │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
Key point

The Fuel Types / EUA Price control belongs in the top-right of the content header, exactly where you highlighted.

Do not put it inside the table.

4. Fuel Types State

When:

● Fuel Types

is selected:

Header

FUEL TYPES

Existing supporting description.

Controls
[ Search                                      ] [Search] [+ ADD FUEL TYPE]
Table
SLNO | Fuel Type | Price per Ton ($) | Carbon | Action

Everything remains as it currently looks.

No redesign.

5. EUA Price State

When the user selects:

○ EUA Price

the content below the header switches.

Header

EUA PRICE

Suggested supporting text:

Manage yearly EUA and VCM pricing used for fuel calculations and reporting.

Controls
[ Search                                      ] [Search] [+ ADD EUA PRICE]
Table
┌──────┬────────┬────────────────┬────────────────┬───────────┬────────┐
│ SLNO │ Year   │ VCM Price Min  │ VCM Price Max  │ EUA Price │ Action │
├──────┼────────┼────────────────┼────────────────┼───────────┼────────┤
│  1   │ 2026   │ 80             │ 120            │ 75        │   ✎    │
│  2   │ 2027   │ 85             │ 125            │ 80        │   ✎    │
│  3   │ 2028   │ 90             │ 130            │ 85        │   ✎    │
└──────┴────────┴────────────────┴────────────────┴───────────┴────────┘

Again, same table styling as Fuel Types.

6. Add EUA Price Modal Blueprint

Click:

+ ADD EUA PRICE

Open the same modal pattern as your existing Add Fuel Details modal.

                 ┌──────────────────────────────┐
                 │  Add EUA Price Details       │
                 │──────────────────────────────│
                 │                              │
                 │  Year*                       │
                 │  ┌────────────────────────┐  │
                 │  │ 2026                   │  │
                 │  └────────────────────────┘  │
                 │                              │
                 │  VCM Price Min*              │
                 │  ┌────────────────────────┐  │
                 │  │ 80                     │  │
                 │  └────────────────────────┘  │
                 │                              │
                 │  VCM Price Max*              │
                 │  ┌────────────────────────┐  │
                 │  │ 120                    │  │
                 │  └────────────────────────┘  │
                 │                              │
                 │  EUA Price*                  │
                 │  ┌────────────────────────┐  │
                 │  │ 75                     │  │
                 │  └────────────────────────┘  │
                 │                              │
                 │       [ CANCEL ]  [ SAVE ]   │
                 └──────────────────────────────┘
Modal rules

Use the existing modal's:

Width
Header height
Gold header
Beige body
Border radius
Input style
Button style
Shadow
Typography
Spacing

Only change the title and fields.

7. Edit Flow

The existing pencil icon remains.

EUA Price Table
       │
       │ Click ✎
       ▼
Edit EUA Price Details
       │
       ├── Year
       ├── VCM Price Min
       ├── VCM Price Max
       └── EUA Price
       │
       ▼
     SAVE
       │
       ▼
Updated table row

For edit mode, the modal title should become:

Edit EUA Price Details

rather than Add EUA Price Details.

8. Interaction Logic

The important behavior is very simple:

                    FUEL CONFIGURATION
                           │
               ┌───────────┴───────────┐
               │                       │
          ● Fuel Types            ○ EUA Price
               │                       │
               ▼                       ▼
       Fuel Types Table          EUA Price Table
               │                       │
          Edit / Add              Edit / Add
               │                       │
               ▼                       ▼
         Fuel Modal              EUA Modal

When switching between the two:

Do not navigate to another page.

The table content simply swaps within the same Fuel Configuration page.

This makes the interaction feel like one configuration module rather than two separate sections.

9. Visual Hierarchy

I would keep the hierarchy exactly like this:

FUEL CONFIGURATION
─────────────────────────────────────────────────────

                                      ● Fuel Types
                                      ○ EUA Price

[ Search ] [ Search ] [ + ADD ... ]

Table
─────────────────────────────────────────────────────

The radio/segmented control should be secondary to the page title, not compete with it.

Given your current UI, I'd use a simple two-option radio group with the existing gold accent, rather than introducing a modern pill/tab component. That will preserve the existing product language.

Final IA
Maintenance
   ↓
Fuel Configuration
   ↓
┌──────────────────────────────────┐
│ Fuel Types  |  EUA Price          │
└──────────────────────────────────┘
       ↓                 ↓
Fuel Types Table     EUA Price Table
       ↓                 ↓
Add/Edit Modal       Add/Edit Modal

This is the cleanest implementation because it requires only structural changes while preserving the existing visual system 100%.