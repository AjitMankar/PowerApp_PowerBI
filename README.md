# DSR Automation — Power Apps + Power BI

Automated Daily Status Report (DSR) system built on Microsoft Power Platform.

## Architecture

```
Power Apps (input) → SharePoint Excel (storage) → Power BI (reporting)
                            ↕
                    Power Automate (notifications)
```

## Repository Structure

```
dsr-automation/
│
├── README.md                        ← This file
│
├── docs/
│   ├── DSR_Full_Implementation_Guide_v2.docx  ← Step-by-step Word guide
│   ├── dsr_flow.md                  ← System flow diagram (Mermaid)
│   ├── dsr_app_design.md            ← Power Apps screen design (Mermaid)
│   └── dsr_data_model.md            ← Excel/SharePoint data model ERD (Mermaid)
│
├── powerapps/
│   └── formulas/
│       ├── app_onstart.fx           ← App.OnStart formula
│       ├── screen1_project.fx       ← Screen 1 formulas
│       ├── screen2_tes.fx           ← Screen 2 formulas
│       ├── screen3_workstreams.fx   ← Screen 3 formulas
│       ├── screen4_issues.fx        ← Screen 4 formulas
│       ├── screen5_defects.fx       ← Screen 5 formulas
│       └── screen6_submit.fx        ← Screen 6 submit formula
│
├── powerbi/
│   └── dax/
│       ├── overall_status.dax       ← RAG status measures
│       ├── test_execution.dax       ← TES measures
│       ├── workstream.dax           ← Workstream measures
│       ├── issues_defects.dax       ← Issue/defect measures
│       └── trends.dax               ← Trend measures
│
└── sharepoint/
    └── DSR_Data_Schema.md           ← All 5 table schemas
```

## Diagrams

### System Flow
See [`docs/dsr_flow.md`](docs/dsr_flow.md)
- Power Apps → SharePoint → Power BI pipeline
- Power Automate notification flows

### App Screen Design
See [`docs/dsr_app_design.md`](docs/dsr_app_design.md)
- All 6 screens + 3 modal screens
- Navigation and collection management
- Key controls per screen

### Data Model
See [`docs/dsr_data_model.md`](docs/dsr_data_model.md)
- 5 SharePoint Excel tables
- Relationships and foreign keys
- All column names and types

## DSR Format Covered

Based on NQE-108 Characteristics Modernization DSR format:

| Section | Power Apps Screen | SharePoint Table |
|---|---|---|
| Project header + Overall RAG | Screen 1 | DSR_Master |
| Test Execution Summary (Passed/Failed/Blocked %) | Screen 2 | Test_Execution_Summary |
| Workstream Summary (TCs + Rally Pass % + Status) | Screen 3 | Workstream_Summary |
| Issues / Risks / Watch-outs / Path to GREEN | Screen 4 | Defects_Issues |
| Open Defects List (DE-XXXXXX + Assignee) | Screen 5 | Open_Defects_List |

## Power BI Pages

| Page | Content |
|---|---|
| Daily DSR | RAG card, Key Highlights, TES metrics |
| Workstream View | TC table with colored status badges, bar chart |
| Issues & Defects | Status table with badges, defect donut chart |
| Trends | Open defects trend, Rally Pass % over time |

## Quick Start

1. **SharePoint** — Create `DSR_Data.xlsx` on your shared drive with all 5 tables
2. **Power Apps** — Create blank canvas app, connect to SharePoint, build 6 screens
3. **Power Automate** — Create instant flow triggered from Power Apps for email notification
4. **Power BI** — Connect to SharePoint Excel, create relationships, add DAX measures, build 4 report pages

See the [full Word guide](docs/DSR_Full_Implementation_Guide_v2.docx) for all formulas and DAX.

## Status Badge Colors (Power BI)

| Status | Text Color | Background |
|---|---|---|
| Green | `#38761D` | `#EAF3DE` |
| Amber | `#BF9000` | `#FAEEDA` |
| Red | `#C00000` | `#FCEBEB` |
| Submitted | `#185FA5` | `#DDEEFF` |
| Closed | `#38761D` | `#EAF3DE` |

Apply via: Format pane → Cell elements → Background color → fx → Field value → select measure
