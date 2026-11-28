# UI Conventions: MySen Platform

Lesson 8 (External Design). Shared visual language, formats, components, error messages, accessibility minimums, design tokens, and component annotation numbering rules across the **MySen Mobile App** and **Admin & Partner Web Portal**.

## 1. Language and tone

- Interface language: Vietnamese by default for Dam Sen Cultural Park visitors and on-site staff; English available in settings (`S-F01-01`). Every message below has both versions in the translation file.
- Address the user as `"bạn"` in Vietnamese (`"you"` in English) with a friendly, welcoming tone.
- Button labels are action verbs that state clearly what happens: `"Thanh toán"`, `"Quét mã QR"`, `"Đổi ưu đãi"`, `"Chỉ đường"`, `"Thử lại"`. Never generic `"OK"` or `"Submit"`.
- Always distinguish **Vé điện tử (E-Ticket)** (purchased with real money in `F-02`) from **Ưu đãi / Voucher (Loyalty Voucher)** (redeemed with earned `Xu` coins in `F-04`).

## 2. Formats

| Item | Format | Example |
|---|---|---|
| Date | `dd/MM/yyyy` | `28/11/2026` |
| Time | `HH:mm`, 24-hour | `09:41` |
| Opening hours | `HH:mm–HH:mm` | `08:00–18:00` |
| Currency (VND) | `#,### đ` (dot thousand separator) | `150.000 đ` |
| Loyalty points | `#,### Xu` (dot thousand separator) | `1.250 Xu` |
| Distance & walking time | `X phút · Y m` (or `km` if $\ge 1000\text{ m}$) | `8 phút · 450 m` |
| Ticket / Voucher ID | Prefix + hyphen + 6 alphanumeric chars | `TKT-8924A1`, `VCH-3049B2` |
| Checkpoint ID | `CP-` + two digits | `CP-01` |

## 3. Components

| Component | When to use | Notes |
|---|---|---|
| Primary button | The one main action of a screen | Full width on mobile (`height: 48px`), `#00875A` fill |
| Secondary button | Alternative or retry actions | Outline style (`1px solid #00875A`) |
| Attraction / Quest card | One landmark, ride, or checkpoint item | Status shown by colour pill AND text label (`Mở cửa` / `Đóng cửa`) |
| Coin pill | Displays visitor's current loyalty balance | Top-right header (`1.250 Xu`), `#FEF3C7` background |
| Banner | Non-blocking warning or status notice | e.g. `"Vị trí của bạn không khả dụng nên bản đồ hiển thị không có vị trí của bạn."` |
| Bottom sheet / Modal | Show POI details, QR code, or badge unlock | Never used for multi-step page navigation |
| Toast | Short confirmation after success | Disappears automatically after 4 seconds |

## 4. Messages

| Situation | Pattern | Example |
|---|---|---|
| Checkpoint outside geofence (`FR-04-02`) | What happened + what to do | `"Bạn đang ở ngoài phạm vi trạm CP-01. Vui lòng di chuyển lại gần điểm tham quan và thử lại."` |
| Invalid or already scanned QR (`FR-04-02`) | What exists + next step | `"Mã QR này không hợp lệ hoặc bạn đã điểm danh trạm này rồi. Hãy khám phá trạm tiếp theo."` |
| Insufficient coins for voucher (`FR-04-07`) | Current gap + how to earn | `"Bạn chưa đủ Xu để đổi ưu đãi này. Hãy điểm danh hằng ngày hoặc hoàn thành thử thách để nhận thêm Xu."` |
| Attraction closed (`FR-03-02`) | Current status + alternative | `"Tàu lượn Hoa Sen hiện đang đóng cửa. Vui lòng chọn điểm tham quan khác trên bản đồ."` |
| Empty search result (`FR-03-01`) | Why + suggested keywords | `"Không tìm thấy kết quả phù hợp. Có phải bạn muốn tìm: Vòng quay Sen Vàng?"` |
| Network / data load error | What happened + retry action | `"Không thể tải dữ liệu. Vui lòng kiểm tra kết nối mạng và thử lại."` |

## 5. Accessibility minimums

- Body text contrast at least `4.5:1` (`WCAG 2.2, 1.4.3`).
- Attraction, ticket, and quest states are never shown by colour alone (`WCAG 2.2, 1.4.1`): open/closed attractions, active/used tickets, and locked/completed checkpoints always combine colour with a clear icon and Vietnamese text label.
- Interactive map pins, buttons, and bottom tab items have a touch target of at least `44 by 44 CSS pixels` (`WCAG 2.2, 2.5.8`).
- Smallest supported mobile viewport width: `375px` (design baseline `390px`); smallest desktop portal width: `1280px` (design baseline `1440px`).

## 6. Design tokens

Every MySen mockup uses only these values. Mobile wireframes are drawn at `390px` (minimum `375px`) and exported at `3x` (`1170px` wide) into `docs/external-design/screens/img/`.

| Token | Value | Used for |
|---|---|---|
| `colour/primary` | `#00875A` | Primary button, active tab, map route line, open status icon |
| `colour/primary-hover` | `#006644` | Primary button pressed state, dark green pill text |
| `colour/primary-soft` | `#E3FCEF` | Open status pill background, selected filter chip |
| `colour/accent` | `#F59E0B` | Loyalty `Xu` coin icon, XP progress bar, star rating |
| `colour/accent-soft` | `#FEF3C7` | Coin balance pill background (`1.250 Xu`), streak banner |
| `colour/text` | `#0F172A` | Screen titles, attraction headings, primary values |
| `colour/text-body` | `#334155` | Body copy, story text, card descriptions |
| `colour/text-muted` | `#64748B` | Subtitles, wait times, walking distance, inactive tabs |
| `colour/border` | `#94A3B8` | Input outlines, secondary button border, back button |
| `colour/border-light` | `#E2E8F0` | Card borders, bottom sheet dividers |
| `colour/surface` | `#F8FAFC` | Main page background, search bar fill |
| `colour/card` | `#FFFFFF` | Card background, bottom sheet, modal, navigation bars |
| `colour/skeleton` | `#E2E8F0` | Loading state placeholders |
| `colour/disabled` | `#CBD5E1` | Disabled primary button background |
| `colour/error-border` | `#DC2626` | Error banner border, closed attraction border |
| `colour/error-text` | `#991B1B` | Error banner text, closed status label |
| `colour/error-bg` | `#FEE2E2` | Error banner background, closed status pill |
| `font/family` | `Be Vietnam Pro`, fallback `Inter`, `Arial` | All UI text across mobile app and web portal |
| `font/size` | title `20px`, heading `16px`, body `14px`, caption `12px`, badge `11px` | Typography scale |
| `space/unit` | `4px`; screen padding `16px`, card gap `12px`, grid gap `8px` | Padding and gaps |
| `radius` | primary button `12px`, banner and card `16px`, input `8px`, bottom sheet `24px`, coin pill `9999px` | Corners |
| `frame/width` | `390px` (mobile app), `1440px` (web portal) | Base frame width for mockups |

Contrast, checked with the WCAG 2.2 formula:

| Pair | Ratio | Needed |
|---|---|---|
| `text #0F172A` on `card #FFFFFF` | `17.9:1` | `4.5:1` (`1.4.3`) |
| `text-body #334155` on `card #FFFFFF` | `10.3:1` | `4.5:1` (`1.4.3`) |
| `text-muted #64748B` on `card #FFFFFF` | `4.8:1` | `4.5:1` (`1.4.3`) |
| `white #FFFFFF` on `primary #00875A` | `4.6:1` | `4.5:1` (`1.4.3`) |
| `error-text #991B1B` on `error-bg #FEE2E2` | `7.2:1` | `4.5:1` (`1.4.3`) |
| `border #94A3B8` on `card #FFFFFF` (input edge) | `3.0:1` | `3:1` (`1.4.11`) |

The disabled button (`white` on `#CBD5E1`) is exempt: `WCAG 1.4.3` does not apply to inactive components.

## 7. Component numbering rules for `<Screen-ID>-numbered.png`

To ensure consistent traceability between mockups and Screen Specs across all team members, every screen must export an annotated image named `<Screen-ID>-numbered.png` into `docs/external-design/screens/img/`.

- **Visual marker style:** Use numbered circles (`24px` diameter, `#2563EB` fill, `#FFFFFF` bold text `12px`) placed adjacent to each interactive or data-bearing component in top-to-bottom, left-to-right reading order (`1`, `2`, `3`...). Note: these markers are reader annotations only, not product UI tokens.
- **Exact 1-to-1 matching:** Every numbered circle `N` on `<Screen-ID>-numbered.png` must correspond to row `#N` in Section 3 (Elements) of `screen-spec-<Screen-ID>.md`, using the exact component name rather than vague descriptions (e.g., write `Close modal button (X)` instead of `"nút đóng mã QR"`).

### Master component numbering map by screen (Team Reference)

| Screen ID | Owner | Annotated File | Standard Numbered Elements (`#1` $\rightarrow$ `#N`) |
|---|---|---|---|
| `S-F00-01` | Hiệp | `S-F00-01-numbered.png` | `#1` App logo & welcome header, `#2` Google OAuth 2.0 button, `#3` Phone/Email input field, `#4` Request OTP primary button, `#5` OTP code input boxes, `#6` Verify & Sign In button |
| `S-F01-01` | Hiệp | `S-F01-01-numbered.png` | `#1` Back button, `#2` User avatar & display name, `#3` Coin & XP summary bar, `#4` Edit profile button, `#5` Language toggle (VI/EN), `#6` Sign out button |
| `S-F02-01` | Nguyệt Minh | `S-F02-01-numbered.png` | `#1` Header & Coin pill, `#2` Visit date selector, `#3` Ticket category filter tabs, `#4` Ticket card & price, `#5` Quantity stepper (`-` / `+`), `#6` Total amount & Continue primary button |
| `S-F02-02` | Nguyệt Minh | `S-F02-02-numbered.png` | `#1` Back button, `#2` Order summary card, `#3` Promo code input & Apply button, `#4` Payment method selector (MoMo / VNPay), `#5` Confirm & Pay primary button |
| `S-F02-03` | Nguyệt Minh | `S-F02-03-numbered.png` | `#1` Ticket status filter (`Còn hiệu lực` / `Đã dùng`), `#2` E-Ticket card, `#3` Dynamic gate QR code, `#4` Ticket ID & validity date, `#5` Brightness boost / Download ticket button |
| `S-F03-01` | Phúc An | `S-F03-01-numbered.png` | `#1` Back button & Coin pill, `#2` Search input & `"Tìm"` button, `#3` Interactive park map canvas & `"Bạn ở đây"` marker, `#4` Attraction pin & status badge (`Mở cửa` / `Đóng cửa`), `#5` POI detail bottom sheet & close (`X`) button, `#6` `"Chỉ đường"` primary button, `#7` Bottom navigation bar |
| `S-F04-01` | Long | `S-F04-01-numbered.png` | `#1` Header & Coin pill, `#2` Quest progress summary bar, `#3` Checkpoint list cards (`CP-01`..`CP-05`), `#4` Scan Checkpoint QR floating/primary button, `#5` Camera viewfinder frame, `#6` Manual checkpoint code fallback button |
| `S-F04-02` | Long | `S-F04-02-numbered.png` | `#1` Back button, `#2` Chapter cover illustration, `#3` Heritage story title & audio guide toggle, `#4` Story body text, `#5` Badge unlock modal & close (`X`) button, `#6` Claim XP & Continue button |
| `S-F04-03` | Bảo Ngân | `S-F04-03-numbered.png` | `#1` Coin balance header, `#2` 7-day streak tracker strip, `#3` Daily check-in primary button, `#4` Bonus mission list cards, `#5` Shortcut button to Voucher Catalog |
| `S-F04-04` | Bảo Ngân | `S-F04-04-numbered.png` | `#1` Coin balance header, `#2` Category filter chips (F&B / Souvenir), `#3` Voucher card & `Xu` cost, `#4` `"Đổi ưu đãi"` primary button, `#5` Active voucher QR modal & close (`X`) button |
| `S-F05-01` | Hương Ly | `S-F05-01-numbered.png` | `#1` Feed filter tabs (`Mới nhất` / `Nổi bật`), `#2` Create post primary button, `#3` Photo upload & caption modal, `#4` Community post card, `#5` Like & Report buttons |
| `S-F05-02` | Hương Ly | `S-F05-02-numbered.png` | `#1` Partner/Service category tabs, `#2` Rental space / Tour package card, `#3` Date & slot picker, `#4` Submit request primary button |
| `S-F06-01` | Hiệp | `S-F06-01-numbered.png` | `#1` Portal sidebar navigation, `#2` KPI summary cards (Visitors, Revenue, Check-ins), `#3` Date range filter, `#4` Visitor flow & revenue chart, `#5` Campaign & Push notification trigger button, `#6` Export reconciliation report button |