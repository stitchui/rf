# Risk Factor Mappings – Implementation Prompt

## Tech Stack
- React
- TypeScript
- MUI
- AG Grid Enterprise

## Objective
Implement Edit, Archive, and Create functionality for the Risk Factor Mappings page.

## Hierarchy
Class → Subclass → Risk Type → Currency → Curve → Risk Factor Rows

Example:
IR → Base → OTC → AED → Swap (21)

## 1. Curve Level Actions
At the curve level, show a vertical three-dot menu.

Actions:
- Edit
- Archive

No Edit action at row level.

Individual rows may optionally support Archive only.

## 2. Edit Mode
When Edit is clicked:

- Rows under the selected curve become editable.
- Show:
  - Cancel button
  - Save button
- Save is disabled initially.
- Save becomes enabled when data changes.
- Cancel discards changes.

## 3. Editable Columns
For now:
- Future Tenor
- Term Code
- Shock Type
- Tenor Dimension

Make the editable columns configurable.

## 4. Read-only Columns
- Class
- Subclass
- Risk Type
- Currency
- Curve Name
- RF ID
- Source controlled fields

## 5. Change Tracking
- Track only changed rows.
- Send only changed rows to backend.
- Include the full row payload.
- Include RF_ID.

## 6. Save API
POST /riskfactor/mappings/edit

Payload:
```json
[
  {
    "...fullChangedRow": true
  }
]
```

## 7. Archive
Curve-level archive:

POST /riskfactor/mappings/archive-curve

Payload:
```json
{
  "rfClassCd": "",
  "rfSubclassCd": "",
  "rfTypeCd": "",
  "currencyCd": "",
  "curveNm": ""
}
```

Row-level archive:

POST /riskfactor/mappings/archive-row

Payload:
```json
{
  "rfId": 100002
}
```

Archive means:
- Update valid_to timestamp.
- No physical deletion.

## 8. Create
Page header button:

+ Create

Open modal:
- Class
- Subclass
- Type
- Curve

Fetch NEVA data and populate grid.

All rows are preselected.

Allow deselection.

## 9. UI Requirements
- MUI Menu
- MUI Dialog
- MUI Button
- Snackbar notifications
- Loading states
- Preserve AG Grid expand/collapse state.
- Only one curve can be edited at a time.
- Prompt when unsaved changes exist.

## 10. Deliverables
- Edit functionality
- Archive functionality
- Create modal
- API service layer
- Strong TypeScript typings
- Reusable components
- Production-ready implementation
