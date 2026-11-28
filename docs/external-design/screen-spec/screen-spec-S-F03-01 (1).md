# Screen Spec: S-F03-01 Interactive Park Map

| Field | Value |
|---|---|
| Screen ID | `S-F03-01` |
| Screen name | Interactive Park Map |
| Actor | Visitor / GenZ Customer |
| Priority | Must (FR-03-01 to FR-03-05 are Must in the FunctionList; see section 9 #2 for FR-03-02 and FR-03-03) |
| Feature | `F-03 Interactive Map & Park Navigation` |
| Activity diagrams | `AD-UC-03` (map and location, search and route, wait-time refresh) |
| Sequence diagram | `S-03` |
| Mockup image | `img/S-F03-01-interactive-map.png` |
| Status | Draft |

Document Owner: Nguyễn Thị Phúc An | Last Updated: 2026-11-22

## 1. Purpose

**Shown when:** The visitor opens the interactive map, from the main menu or from "Open Park Map" on `S-F04-03`, to see the 2.5D/3D park map with points of interest (POIs), see their own position, search for an attraction or POI, check an attraction's wait time and status, and get walking directions.

**The user leaves this screen when:** The visitor goes back to the Main Menu. The search, the attraction details and the route are shown on this screen (as results, a bottom sheet and a map overlay), so they do not open another screen.

**Source trace:** `AD-UC-03` nodes `s3, r1` (load and render the map), `s1, d1, s2, g1, p1, d3` (location permission and live position), `a2, s7, d2, s8-s11` (search), `a3, g2, s12` (walking route), `t2, w1, d4, w2, w3` (wait-time and status refresh). The Staff update flow (`start2, st1, s13, s14, st2`) is on `S-F03-02`, not here.

## 2. Mockup

![S-F03-01](img/S-F03-01-interactive-map.png)

![Attraction details and route](img/S-F03-01-attraction-route.png)

> Sample data only. Attraction names, wait times and distances in the image are illustrative.

Layout overview:

- **Top bar:** Back button | title "Interactive Map".
- **Search bar:** Text input and search button, under the top bar.
- **Map area:** The 2.5D/3D park map with POI markers, the visitor's position marker, and the route line when a route is shown. A short notice appears over the map when the visitor's position is not available.
- **Search results panel:** Matching attractions and POIs. For a failed search it shows the not-found message with similar names, the "currently closed" message, or the error message with "Try Again".
- **Attraction details sheet:** A bottom sheet with the attraction name, Open / Closed status, wait time, walking time, and the screen's single primary button "Get Directions".
- **Route summary:** Walking time and distance for the selected route.

## 3. Element inventory

| # | Element | Type | Content / data source | Required | Validation |
|---|---|---|---|---|---|
| 1 | `MapTopBar` | Header | Back button, title "Interactive Map" | Yes | Back returns to the Main Menu |
| 2 | `SearchInput` | Text input | Placeholder "Search attractions or places" (FR-03-03) | Yes | Trimmed, non-empty text to submit; maximum length [NEEDS CLARIFICATION: not defined] |
| 3 | `SearchSubmitButton` | Icon button | Label "Search" (FR-03-03) | Yes | Disabled while `SearchInput` is empty |
| 4 | `ParkMapCanvas` | Map | 2.5D/3D park map (FR-03-01); data from the MySen backend through the map SDK | Yes | Shows the whole park on open; rendered by the Map SDK |
| 5 | `PoiMarkerLayer` | Map markers | POI and attraction markers from the POI list (FR-03-01) | Yes | One marker per available POI; icon plus text label, not colour alone |
| 6 | `CurrentPositionMarker` | Map marker | "You are here" marker at the visitor's current coordinates (FR-03-02) | No | Only when location permission is granted and a position was obtained; moves while the screen is open; removed when the screen closes |
| 7 | `LocationUnavailableNotice` | Banner | "Your location is not available, so the map is shown without your position." (FR-03-02) | No | Only when location permission is denied |
| 8 | `SearchResultList` | List | Matching attractions and POIs: name, location, status, wait time, walking time (FR-03-03) | No | Shown after a search with a match. Walking time shown only when a current position is available |
| 9 | `NotFoundMessage` | Banner | "We couldn't find “{query}”. Did you mean:" (FR-03-03) | No | Only when no attraction or POI matches |
| 10 | `SimilarNameList` | List | Names similar to the query (FR-03-03) | No | Only with `NotFoundMessage`; selecting a name searches for it |
| 11 | `ClosedAttractionMessage` | Banner | "{attraction name} is currently closed." (FR-03-03, FR-03-05) | No | Only when the matching attraction has status Closed; no route is offered |
| 12 | `SearchErrorBanner` | Banner | "Unable to load data. Please try again." (FR-03-03) | No | Only when the data source is unavailable or returns an error; never shows partial or misleading results |
| 13 | `RetrySearchButton` | Text button | "Try Again" | No | Only with `SearchErrorBanner`; repeats the same search |
| 14 | `AttractionDetailsSheet` | Bottom sheet | Attraction name, location, `AttractionStatusBadge`, `WaitTimeText`, `WalkingTimeText`, `GetDirectionsButton`, close control | No | Opens for one attraction at a time; while it is open, wait time and status refresh (FR-03-05) |
| 15 | `AttractionStatusBadge` | Badge | "Open" or "Closed" (FR-03-05) | Yes (in the sheet) | Text plus icon, not colour alone |
| 16 | `WaitTimeText` | Text | Latest wait time, e.g. "25 min" (FR-03-05) | No | Shown when status is Open; replaced by the Closed status when the attraction is closed. Wait time is never added to walking time |
| 17 | `WalkingTimeText` | Text | Estimated walking time from the visitor's position, e.g. "8 min walk" (FR-03-03, FR-03-04) | No | Only when a current position is available |
| 18 | `GetDirectionsButton` | Primary button | "Get Directions" (FR-03-04) | No | Shown only when the attraction is Open and a current position is available; opens the route on this screen |
| 19 | `RouteLine` | Map overlay | Walking route from the visitor's position to the selected destination (FR-03-04) | No | Calculated on the device by the map SDK |
| 20 | `RouteSummaryCard` | Card | Walking time and distance, e.g. "8 min · 450 m" (FR-03-04) | No | Shown together with `RouteLine` |
| 21 | `BottomNavigation` | Shared app navigation | MySen / Tickets / Rewards / Account | Yes | Shared shell; route owner and active tab to confirm |
| 22 | `FeatureLabel` | Text | "F-03 · Interactive Map" (mockup annotation only) | No | Not shown in the built app |

## 4. States

| State | What the user sees | Trigger |
|---|---|---|
| Default | Map with POI markers, search bar, the position marker (if location is allowed), no sheet or results | Visitor opens the screen; map data loads; location permission is granted |
| Location not allowed | Same map and POIs, no position marker, `LocationUnavailableNotice`; no walking time and no "Get Directions" | Visitor denies location permission |
| Loading | Map placeholder until the map is drawn; a small spinner in the results panel while a search runs | Screen opens; visitor submits a search |
| Empty (search finds nothing) | `NotFoundMessage` with `SimilarNameList`; the map stays visible | Search returns no match |
| Attraction closed | `ClosedAttractionMessage` for a searched attraction, or status "Closed" in the details sheet; no wait time, no "Get Directions" | The matching or opened attraction has status Closed |
| Error | Search: `SearchErrorBanner` with "Try Again". Map data fails to load at open: message and recovery [NEEDS CLARIFICATION: see section 9 #9] | Data source unavailable or returns an error |
| Success / confirmation | Search with a match: result with location, status, wait time, walking time. Route requested: `RouteLine` and `RouteSummaryCard` (walking time and distance). Details sheet open: wait time and status refresh | Search matches an Open attraction; route calculated; refresh succeeds |

## 5. Interactions and navigation

| # | Element | User action | System response | Goes to screen |
|---|---|---|---|---|
| 1 | Screen | Open the screen | Loads map data and the POI list, renders the 2.5D/3D map with POIs (FR-03-01), then requests location permission. Granted → gets the current position, shows `CurrentPositionMarker` and keeps updating it while the screen is open (FR-03-02). Denied → keeps the map without a position marker and shows `LocationUnavailableNotice` | stays |
| 2 | `SearchInput` + `SearchSubmitButton` | Type a name and tap "Search" | Queries POI and attraction data (FR-03-03). Data unavailable → `SearchErrorBanner`. No match → `NotFoundMessage` and `SimilarNameList`. Match, attraction Closed → `ClosedAttractionMessage`, no route offered. Match, attraction Open → `SearchResultList` with location, status, wait time, walking time | stays |
| 3 | `SimilarNameList` | Tap a suggested name | Searches for that name, as in row 2 | stays |
| 4 | `RetrySearchButton` | Tap "Try Again" | Repeats the search | stays |
| 5 | `SearchResultList` item or `PoiMarkerLayer` marker | Tap | Opens `AttractionDetailsSheet` for that attraction. While the sheet is open, refreshes wait time and status periodically (FR-03-05): Open → shows the wait time; Closed → shows "Closed" | stays |
| 6 | `AttractionDetailsSheet` | Close the sheet | Closes the sheet and stops the refresh for that attraction | stays |
| 7 | `GetDirectionsButton` | Tap "Get Directions" | The map SDK calculates the walking route on the device from the current position to the attraction. Shows `RouteLine` and `RouteSummaryCard` (walking time and distance) (FR-03-04) | stays |
| 8 | `MapTopBar` back button | Tap | Stops position updates and returns to the previous screen | Main Menu |
| 9 | Staff update (system event on another screen) | — | Not an action on this screen. A wait time or status saved on `S-F03-02` appears here at the next refresh or search | stays |

## 6. Screen-level rules

| Rule ID | Rule | Source |
|---|---|---|
| SR-001 | The park map and POI list come from the MySen backend. The visitor's position and the walking route are calculated on the device by the map SDK. | FR-03-01; FR-03-04 (client-side routing); `S-03` |
| SR-002 | The position marker is shown only while location permission is granted. It updates while this screen is open and stops when the screen closes. Without permission the map and POIs still work. | FR-03-02; `AD-UC-03 d1, d3` |
| SR-003 | A search ends in exactly one outcome: error, no match, match with attraction Closed, or match with attraction Open. A failed or empty search never shows misleading results. | FR-03-03; `AD-UC-03 d2` |
| SR-004 | A route is offered only for an Open attraction, and only when a current position is available. | FR-03-04; `AD-UC-03 s11, s12` |
| SR-005 | Walking time and wait time are separate values. Each is shown on its own and they are never added together. | `S-03` note |
| SR-006 | While an attraction is being viewed, wait time and status refresh periodically. A closed attraction shows its Closed status instead of a wait time. | FR-03-05; `AD-UC-03 t2, w1, d4` |
| SR-007 | Wait time and status are saved by Staff on `S-F03-02`. This screen depends on those stored values only: a Staff update is seen at the next refresh or search, not instantly. | FR-03-06; `AD-UC-03 s13` |
| SR-008 | Numbers use `#,###`; wait time and walking time are shown in minutes; buttons use verb-first labels; one primary button per screen ("Get Directions"). | UI Conventions |
| SR-009 | Status and position are never carried by colour alone: Open / Closed and the "You are here" marker have a text label or icon. | UI Conventions |

## 7. Linked requirements

| FR ID | Priority | What this screen does for it |
|---|---|---|
| FR-03-01 | Must | Shows the 2.5D/3D park map and the POI markers |
| FR-03-02 | Must | Shows and updates the visitor's position marker while the screen is open and permission is available |
| FR-03-03 | Must | Provides search and shows matching attractions and POIs, the not-found message with similar names, the closed message and the retry message |
| FR-03-04 | Must | Shows the walking route, walking time and distance after "Get Directions" |
| FR-03-05 | Must | Shows and refreshes the wait time and Open / Closed status of the attraction being viewed |
| FR-03-06 | Must | Not on this screen; see `S-F03-02`. This screen shows the values it saves |

## 8. Responsive and accessibility notes

- Smallest supported width: 360px. The search bar and top bar stay on one row; the details sheet covers at most half of the map height so the position marker stays visible.
- Mobile: the map takes the full width. The details sheet slides up from the bottom. "Get Directions" is inside the sheet, within thumb reach.
- Tablet / desktop web: two columns, with search, results and attraction details on the left and the map on the right; content width capped at 960px.
- Information never carried by colour alone: status, position and route have a text label or icon.
- Wait-time and status changes, and the "currently closed" message, are announced to screen readers (live region). Tap targets at least 48 × 48 dp on mobile; body text contrast at least 4.5:1. Map markers and the details sheet are reachable by keyboard and screen-reader focus; closing the sheet returns focus to the marker or result that opened it.

## 9. Open questions

| # | Question | Blocking? | Status |
|---|---|---|---|
| 1 | [NEEDS CLARIFICATION: the Screen List was not provided. `S-F03-01` is taken from the link on `S-F04-03`. Should search, attraction details and route be separate screens, or stay on this one screen as sheets and overlays? The Staff update screen is assumed to be `S-F03-02`.] | No | Open (drawn as one screen) |
| 2 | [NEEDS CLARIFICATION: priority. The FunctionList lists FR-03-02 and FR-03-03 as Must; the cost sheet lists FR-03-02 as Should and FR-03-03 as Could. Which is correct?] | No | Open (Must used) |
| 3 | [NEEDS CLARIFICATION: when location permission is denied, FR-03-02 defines no outcome and no FR says the app prompts the visitor to enable location (same as `AD-UC-03` section 6 #1).] | No | Open (info notice only, no prompt) |
| 4 | [NEEDS CLARIFICATION: FR-03-04 needs a current location. What does the visitor get when it is unavailable (permission denied or no GPS fix)? Same as `AD-UC-03` section 6 #4.] | Yes | Open (button hidden) |
| 5 | [NEEDS CLARIFICATION: the refresh interval for position and for wait time is not defined in FR-03-02 and FR-03-05.] | No | Open |
| 6 | [NEEDS CLARIFICATION: no FR says how a visitor opens an attraction's details (marker, result), closes the sheet, or clears a route or a search.] | No | Open (marker or result opens the sheet; sheet has a close control; route and search clearing not drawn) |
| 7 | [NEEDS CLARIFICATION: `AD-UC-03` ends at "currently closed" and offers no route. If a visitor opens a closed attraction from a marker, is "Get Directions" hidden?] | No | Open (hidden) |
| 8 | [NEEDS CLARIFICATION: must the visitor be signed in to use the map?] | No | Open (no sign-in rule assumed) |
| 9 | [NEEDS CLARIFICATION: what does the visitor see if the map data cannot be loaded at open, or GPS / Beacon returns no position? FR-03-03 covers errors only for search.] | No | Open (same as `AD-UC-03` section 6 #5) |
| 10 | [NEEDS CLARIFICATION: FR-03-03 says "available details". Do search results include wait time and walking time, as sequence step 20 shows?] | No | Open (shown, as in `AD-UC-03` section 6 #9) |
