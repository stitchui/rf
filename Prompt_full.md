Here is a ready-to-use prompt you can give to Claude Code, Cursor, or v0:

Implement Risk Factor Mappings Edit and Archive functionality using React, TypeScript, MUI, and AG Grid Enterprise.

Current page:

* Risk Factor Mappings page uses AG Grid Enterprise with grouped hierarchy.
* Group hierarchy:
  Class → Subclass → Risk Type → Currency → Curve → Risk Factor rows
* Example:
  IR → Base → OTC → AED → Swap (21) → rows like USSTS.IR_AED_Swap.2M

Requirements:

1. Curve Level Actions

* At the curve level, show a vertical three-dot action menu.
* Menu options:

  * Edit
  * Archive
* Do not show Edit on individual risk factor rows.
* Individual rows should only have Archive action if row-level archive is supported.

2. Edit Mode

* When user clicks Edit at curve level, only the rows under that selected curve should become editable.
* Replace or supplement the curve-level action area with:

  * Cancel button
  * Save button
* Save should be disabled initially.
* Save should become enabled only when at least one editable value changes.
* Cancel should discard all unsaved changes and return grid to view mode.

3. Editable Columns
   For now, make these columns editable:

* Future Tenor
* Term Code
* Shock Type
* Tenor Dimension

Keep these columns read-only:

* Class
* Subclass
* Risk Type
* Currency
* Curve Name
* RF ID
* Name
* NEVA/source-controlled fields

Make the editable column list configurable in the frontend so it can be adjusted later.

4. Change Tracking

* Track only changed rows.
* On Save, send only changed rows to backend.
* Payload should include the full row object, not only RF_ID.
* Use the same data shape as the existing grid/API response.
* Include RF_ID in every changed row.

5. Save API
   Create a placeholder service function:

POST /riskfactor/mappings/edit

Payload:
[
{
...fullChangedRow
}
]

Backend behavior expected:

* Backend will use RF_ID and active valid_to timestamp to update/archive old version and insert a new active version.
* Frontend only needs to send changed row data.

6. Archive Functionality
   Curve-level archive:

* User clicks Archive from curve-level menu.
* Show confirmation modal:
  “Are you sure you want to archive this curve and all related risk factor rows?”
* On confirm, send hierarchy payload:
  {
  rfClassCd,
  rfSubclassCd,
  rfTypeCd,
  currencyCd,
  curveNm
  }

Endpoint placeholder:
POST /riskfactor/mappings/archive-curve

Row-level archive, if implemented:

* Show Archive action only on leaf rows.
* Confirmation modal:
  “Are you sure you want to archive this risk factor?”
* Payload:
  {
  rfId
  }

Endpoint placeholder:
POST /riskfactor/mappings/archive-row

Archive means backend updates valid_to to current timestamp. Do not delete rows from frontend directly unless API succeeds.

7. UI Behavior

* Use MUI Menu for the three-dot actions.
* Use MUI Button for Save and Cancel.
* Use MUI Dialog for archive confirmation.
* Show Save and Cancel on the selected curve row when edit mode is active.
* Keep UX close to existing US SPARC styling.
* Highlight edited cells or edited rows subtly.
* Show loading state while saving/archive API is in progress.
* Show success/error toast/snackbar after API response.

8. AG Grid Behavior

* Only one curve can be in edit mode at a time.
* If user tries to edit another curve while unsaved changes exist, show confirmation dialog:
  “You have unsaved changes. Do you want to discard them?”
* Use AG Grid transaction/update APIs where appropriate.
* Preserve expand/collapse state after save.
* Refresh data after successful save/archive if needed.

9. Data Mapping
   Grid data includes fields similar to:

* rfId
* rfNm
* altRfNm
* rfClassCd
* rfSubclassCd
* rfTypeCd
* currencyCd
* curveNm
* curveInstrumentTypeNm
* clearingHouseCd
* futureTenorCd
* termCd
* shockTypeCd
* tenorDimensionCd
* validFromTs
* validToTs
* sourceNm

Please inspect the existing codebase and adapt to the actual field names.

10. Deliverables

* Update the existing Risk Factor Mappings component.
* Add reusable action menu component if helpful.
* Add edit mode state management.
* Add changed-row tracking.
* Add save/cancel behavior.
* Add archive confirmation dialog.
* Add placeholder API service methods.
* Keep code clean, strongly typed, and compatible with React + TypeScript + MUI + AG Grid Enterprise.
