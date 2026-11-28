# Screen Spec: S-F03-02 Update Wait Time & Status

| Field | Value |
|---|---|
| Screen ID | `S-F03-02` |
| Screen name | Update Wait Time & Status |
| Actor | Staff & Admin (authorised operation staff) |
| Priority | Must (FR-03-06) |
| Feature | `F-03 Interactive Map & Park Navigation` |
| Activity diagrams | `AD-UC-03` (Staff update flow: `start2, st1, s13, s14, st2`) |
| Sequence diagram | `S-03` (Operation Staff Updates Wait Time, external) |
| Mockup image | `img/S-F03-02-update-wait-time.png` |
| Status | Draft |

Document Owner: Nguyễn Thị Phúc An | Last Updated: 2026-11-22

## 1. Purpose

**Shown when:** Authorised operation staff open the admin interface to enter the current wait time and the open / closed status of an attraction, so that visitors see the latest values on `S-F03-01`.

**The user leaves this screen when:** The staff member saves an update and sees the confirmation, or closes the admin interface. No visitor screen is opened from here.

**Source trace:** `AD-UC-03` nodes `start2, st1` (Staff submits the update), `s13` (save), `s14, st2` (confirmation). Visitors read the saved values in `AD-UC-03` nodes `s7, w1` on `S-F03-01`.

## 2. Mockup

![S-F03-02](img/S-F03-02-update-wait-time.png)

> Sample data only. Attraction names and values in the image are illustrative.

Layout overview:

- **Top bar:** Title "Update Wait Time & Status".
- **Attraction selector:** The attraction to update.
- **Update form:** Status (Open / Closed) and wait time in minutes.
- **Primary button:** "Save Update", fixed at the bottom of the form.
- **Confirmation:** A message that the update was saved.

## 3. Element inventory

| # | Element | Type | Content / data source | Required | Validation |
|---|---|---|---|---|---|
| 1 | `UpdateTopBar` | Header | Title "Update Wait Time & Status" | Yes | None |
| 2 | `AttractionSelect` | Dropdown | List of attractions from the attraction data (FR-03-06) | Yes | One attraction must be selected |
| 3 | `CurrentValuesText` | Text | The wait time and status currently stored for the selected attraction | No | Read-only; shown after an attraction is selected |
| 4 | `StatusSelect` | Segmented control | "Open" / "Closed" (FR-03-06) | Yes | Exactly one value; allowed values only |
| 5 | `WaitTimeInput` | Number input | Wait time in minutes, e.g. "25" (FR-03-06) | Yes when status is Open | Whole number; allowed range [NEEDS CLARIFICATION: not defined]; not required when status is Closed |
| 6 | `SaveUpdateButton` | Primary button | "Save Update" (FR-03-06) | Yes | Disabled until an attraction and a valid status are chosen |
| 7 | `UpdateSavedMessage` | Banner | "Update saved. Visitors will see the new values at their next refresh." (FR-03-06) | No | Shown after the system confirms the save |
| 8 | `UpdateErrorMessage` | Banner | "We couldn't save the update. Please try again." | No | Shown when the save fails or the update is rejected (see section 9 #3) |
| 9 | `FeatureLabel` | Text | "F-03 · Interactive Map" (mockup annotation only) | No | Not shown in the built app |

## 4. States

| State | What the user sees | Trigger |
|---|---|---|
| Default | Attraction selector, empty form, "Save Update" disabled | Staff open the screen |
| Empty (no data) | Selector empty with "No attractions available" [NEEDS CLARIFICATION: wording and case not defined] | No attraction data |
| Loading | "Save Update" shows a spinner and is disabled; the form is locked | Staff tap "Save Update" |
| Error | `UpdateErrorMessage`; the form keeps the entered values; stored values do not change | Save fails, or the update is rejected |
| Success / confirmation | `UpdateSavedMessage`; `CurrentValuesText` shows the new values | The system saves the update and confirms |

## 5. Interactions and navigation

| # | Element | User action | System response | Goes to screen |
|---|---|---|---|---|
| 1 | `AttractionSelect` | Choose an attraction | Shows the values currently stored for it in `CurrentValuesText` | stays |
| 2 | `StatusSelect` | Choose Open or Closed | Closed → the wait time field is not required; Open → a wait time is required | stays |
| 3 | `SaveUpdateButton` | Tap "Save Update" | Validates the update, saves wait time and status, and confirms (FR-03-06). Visitors see the new values at their next refresh or search | stays |
| 4 | Screen (not authorised) | Open the screen without staff authorisation | The update is not allowed [NEEDS CLARIFICATION: see section 9 #3] | [NEEDS CLARIFICATION: not defined] |

## 6. Screen-level rules

| Rule ID | Rule | Source |
|---|---|---|
| SR-001 | Only authorised operation staff can submit an update. | FR-03-06 (authorisation row) |
| SR-002 | The update is validated before saving; only the allowed fields (attraction, status, wait time) can be changed. | FR-03-06 (BE rows) |
| SR-003 | The save is confirmed to the staff member only after the system has stored the values. | FR-03-06; `AD-UC-03 s14` |
| SR-004 | This screen and `S-F03-01` are not connected by a control flow. The staff update reaches visitors only through the stored values, which `S-F03-01` reads at its next refresh or search. | `AD-UC-03` reading notes |
| SR-005 | Wait time is a whole number of minutes, shown in the format `#,###`; buttons use verb-first labels; one primary button per screen ("Save Update"). | UI Conventions |

## 7. Linked requirements

| FR ID | Priority | What this screen does for it |
|---|---|---|
| FR-03-06 | Must | Lets authorised operation staff enter the wait time and open / closed status, saves them, and confirms the save |

## 8. Responsive and accessibility notes

- Smallest supported width: 360px. The form is one column; "Save Update" is fixed at the bottom of the form.
- Tablet / desktop web: the form is centred, content width capped at 640px.
- Information never carried by colour alone: Open / Closed has a text label.
- Success and error messages are announced to screen readers (live region). Tap targets at least 48 × 48 dp; body text contrast at least 4.5:1.

## 9. Open questions

| # | Question | Blocking? | Status |
|---|---|---|---|
| 1 | [NEEDS CLARIFICATION: is this a screen inside the MySen app, or a page of the separate admin system shown as "external" in `S-03`? FR-03-06 calls it "the operation-staff interface".] | No | Open (drawn as a staff screen) |
| 2 | [NEEDS CLARIFICATION: allowed range for the wait time, and whether Staff can enter a wait time while the status is Closed.] | No | Open |
| 3 | [NEEDS CLARIFICATION: what does the staff member see when the update is rejected or the person is not authorised? FR-03-06 has an authorisation and validation row but no outcome (same as `AD-UC-03` section 6 #8).] | No | Open (generic error message) |
| 4 | [NEEDS CLARIFICATION: the staff role is named "Staff & Admin", "operation staff" and "Operation / Ride Staff" in different documents. Which name is on the Context Diagram?] | No | Open (same as `AD-UC-03` section 6 #6) |
| 5 | [NEEDS CLARIFICATION: the Screen List was not provided, so `S-F03-02` is an assumed ID.] | No | Open |
