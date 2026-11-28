# UI Conventions & Design Tokens: MySen Platform

Lesson 8 (External Design). Shared visual language, design tokens, formatting rules, component standards, and asset naming conventions across the **MySen Mobile App** (`375px` / `390px` mobile viewport) and **Admin & Partner Web Portal** (`1440px` desktop viewport). Every `screen-spec-S-Fxx-nn.md` must follow the exact numeric tokens defined below.

| Field | Value |
| --- | --- |
| Version | v2.0 |
| Applies to | `screen-list.md`, `screen-transition.md`, all `docs/external-design/screens/screen-spec-*.md` |

---

## 1. Language & Microcopy Standards

* **Primary UI Language:** Vietnamese (concise, friendly, action-oriented phrasing tailored for Dam Sen Cultural Park visitors and on-site staff).
* **Secondary Language:** English (selectable via Account Settings `S-F01-01`).
* **Tone & Terminology:**
  * Always distinguish **Vé điện tử (E-Ticket)** (purchased with real money in `F-02`) from **Ưu đãi / Voucher (Loyalty Voucher)** (redeemed using earned `Xu` / Coins in `F-04`).
  * Use consistent action labels: `"Thanh toán"`, `"Quét mã QR"`, `"Đổi ưu đãi"`, `"Chỉ đường"`, `"Thử lại"`.

---

## 2. Data Formatting Rules

| Data Type | Format Pattern | Valid Example | Invalid Example |
| --- | --- | --- | --- |
| Date | `dd/MM/yyyy` | `28/11/2026` | `2026-11-28`, `11/28/26` |
| Time (24-hour) | `HH:mm` | `09:41`, `18:30` | `9:41 AM`, `6:30 PM` |
| Date & Time | `HH:mm - dd/MM/yyyy` | `14:00 - 28/11/2026` | `28/11/2026 2pm` |
| Currency (VND) | `#,### đ` (dot thousand separator) | `150.000 đ`, `1.250.000 đ` | `150,000 VND`, `150k` |
| Loyalty Points | `#,### Xu` (dot thousand separator) | `1.250 Xu`, `500 Xu` | `1250 coins`, `1.25k Xu` |
| Distance & Duration | `X phút · Y m` (or `km` if $\ge 1000\text{ m}$) | `8 phút · 450 m` | `8 mins / 0.45km` |
| Phone Number (VN) | `0XXX XXX XXX` (10 digits) | `0901 234 567` | `+84-901234567` |

---

## 3. Color Palette (Design Tokens)

All screen mockups and CSS/Tailwind styles must use only the following Hex color values:

| Token Name | Role & Usage | Hex Code | Contrast / Notes |
| --- | --- | --- | --- |
| `color-primary` | Brand Primary (Dam Sen Lotus Green) — primary buttons, active tabs, route paths | `#00875A` | White text `#FFFFFF` |
| `color-primary-hover` | Primary Pressed / Hover state | `#006644` | White text `#FFFFFF` |
| `color-primary-soft` | Primary Tint Background — active badges, selected cards | `#E3FCEF` | Dark green text `#006644` |
| `color-accent` | Loyalty & Gamification Gold — `Xu` coin badges, XP bars, star ratings | `#F59E0B` | Dark text `#0F172A` |
| `color-accent-soft` | Loyalty Tint Background — coin pill (`1.250 Xu`), streak banners | `#FEF3C7` | Dark amber text `#92400E` |
| `color-bg-page` | Main Screen Canvas Background | `#F8FAFC` | Light slate gray |
| `color-bg-surface` | Card, Bottom Sheet, Modal, Header & Tab Bar Surface | `#FFFFFF` | Pure white |
| `color-border` | Card borders, input outlines, dividers | `#E2E8F0` | `1px` solid |
| `color-text-primary` | Headings, primary body copy, active values | `#0F172A` | High contrast |
| `color-text-secondary` | Subtitles, metadata, timestamps, inactive tab labels | `#64748B` | Medium contrast |
| `color-text-muted` | Placeholders, disabled labels | `#94A3B8` | Low contrast |
| `color-success` | Open attraction status (`Mở cửa`), valid QR check-in | `#16A34A` | Soft bg `#DCFCE7` |
| `color-warning` | GPS unavailable notice, streak-at-risk alert | `#D97706` | Soft bg `#FEF3C7` |
| `color-error` | Closed attraction (`Đóng cửa`), load failure, invalid QR | `#DC2626` | Soft bg `#FEE2E2` |

---

## 4. Typography Scale

* **Font Family:** `Be Vietnam Pro` (fallback: `Inter`, `-apple-system`, `sans-serif`) — chosen for full Vietnamese diacritic legibility on mobile screens.

| Token Name | Element Role | Font Size | Font Weight | Line Height | Letter Spacing |
| --- | --- | --- | --- | --- | --- |
| `type-h1` | Screen Page Title / Portal Header | `20px` | `700` (Bold) | `28px` | `-0.01em` |
| `type-h2` | Section Heading / Bottom Sheet Title | `18px` | `700` (Bold) | `24px` | `-0.01em` |
| `type-h3` | Card Title / Attraction Name / Quest Name | `16px` | `600` (SemiBold) | `22px` | `0em` |
| `type-body` | Standard Body Text / Story Content | `14px` | `400` (Regular) | `20px` | `0em` |
| `type-body-bold` | Emphasized Body / Button Label / Price | `14px` | `600` (SemiBold) | `20px` | `0em` |
| `type-caption` | Metadata, Wait Time, Distance, Helper Text | `12px` | `400` (Regular) | `16px` | `0.01em` |
| `type-badge` | Status Pills (`Mở cửa`, `Đóng cửa`), Tab Bar Labels | `11px` | `600` (SemiBold) | `14px` | `0.02em` |

---

## 5. Layout, Spacing & Shape Tokens

### 5.1 Frame Dimensions
* **Visitor Mobile App (`S-F00` to `S-F05`):**
  * Design Frame Width: `390px` (minimum supported width: `375px`).
  * Safe Area Top (Status Bar): `44px`; Top Navigation Bar Height: `56px`.
  * Bottom Tab Bar Height: `64px` + `20px` home indicator safe area (`84px` total).
* **Admin & Partner Web Portal (`S-F05-03`, `S-F06-01`):**
  * Design Frame Width: `1440px` (minimum desktop breakpoint: `1280px`).
  * Left Sidebar Width: `240px`; Top Header Height: `64px`; Content Max Width: `1200px`.

### 5.2 Spacing Scale (`4px` Base Grid)
| Token | Value | Standard Usage |
| --- | --- | --- |
| `space-xs` | `4px` | Icon-to-label gap inside pills/badges |
| `space-sm` | `8px` | Vertical gap between related text lines; inner badge padding |
| `space-md` | `12px` | Gap between list cards; form field internal padding |
| `space-lg` | `16px` | Standard horizontal screen margin (`padding-left/right: 16px`); card padding |
| `space-xl` | `24px` | Section-to-section vertical spacing; modal padding |

### 5.3 Border Radius & Elevation
| Token | Value | Standard Usage |
| --- | --- | --- |
| `radius-sm` | `8px` | Input fields, small status badges, thumbnail images |
| `radius-md` | `12px` | Primary CTA buttons (`height: 48px`), inner stat boxes |
| `radius-lg` | `16px` | Content cards, attraction info cards, error banners |
| `radius-sheet` | `24px` | Top corners of Bottom Sheets and Modals (`24px 24px 0 0`) |
| `radius-full` | `9999px` | Coin pills (`1.250 Xu`), search bars, user avatars, map pins |
| `shadow-card` | `0 2px 8px rgba(15, 23, 42, 0.06)` | Floating cards over map canvas |
| `shadow-sheet` | `0 -4px 16px rgba(15, 23, 42, 0.10)` | Bottom sheet overlay |

---

## 6. Shared Navigation & Component Conventions

1. **Top App Bar (Mobile):**
   * Left: Back button (`<`, `24x24px` touch target `44x44px`) + `MS` Brand Avatar (`28x28px`, `#00875A`) + Screen Title (`type-h1`).
   * Right: Coin Balance Pill (`1.250 Xu`, `#FEF3C7`) + User Avatar (`32x32px`).
2. **Bottom Navigation Bar (Mobile — 4 Fixed Tabs):**
   * Tab 1: `MySen` (Home / Quests / Map hub)
   * Tab 2: `Vé` (E-Ticket Catalog & QR Wallet)
   * Tab 3: `Ưu đãi` (Loyalty Coin Store & My Vouchers)
   * Tab 4: `Tài khoản` (Profile, Badges & Settings)
   * Active tab uses `#00875A` icon + `type-badge` text; inactive tabs use `#64748B`.
3. **Standard States Required per Screen Spec:**
   * Every Screen Spec must define **Default**, **Empty**, **Loading**, and **Error** states.
   * Error banners use `#FEE2E2` background, `1px solid #FECACA` border, `#DC2626` message text, and an inline `"Thử lại"` action button (`#00875A`).

---

## 7. Image Naming & Component Numbering Convention (`*-numbered.png`)

To ensure strict traceability between Figma/Canva mockups and `screen-spec-S-Fxx-nn.md` (Section 3 Elements & Section 6 Screen Rules):

1. **File Naming in `docs/external-design/screens/img/`:**
   * Clean default mockup: `<Screen-ID>.png` (e.g., `S-F04-01.png`)
   * Annotated component map: `<Screen-ID>-numbered.png` (e.g., `S-F04-01-numbered.png`)
   * Additional UI states: `<Screen-ID>-<state-slug>.png` in lowercase kebab-case (e.g., `S-F03-01-load-error.png`)
2. **Component Numbering Rules (`*-numbered.png`):**
   * Every interactive control, input field, dynamic data display, and navigation element on `<Screen-ID>-numbered.png` must be marked with a circular numbered badge (`1`, `2`, `3`, ... in top-to-bottom, left-to-right reading order).
   * Each number `#` in the image must correspond **1-to-1** with row `#` in Section 3 (**Elements**) of `screen-spec-<Screen-ID>.md`, specifying exact component ID, type, data source, target screen/action, and local validation rules (`SR-001`, `SR-002`, ...).