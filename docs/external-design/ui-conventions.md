# UI Conventions: Dien Hong System

> Version 3.1 (20/11/2026). Layout taken from the reference screens of an existing nursing-home
> system (EHS: the "presence in the ward" list and the vital-signs dialog) and adapted to this
> repository. Content, wording and dates aligned with the client's website dienhongfamilycare.vn
> (page "Viện dưỡng lão", read on 18/11/2026). Colours from the Diên Hồng FamilyCare brand
> identity (palette given by the team on 18/11/2026); all values live in
> [design-tokens.css](design-tokens.css). Screens, components and messages follow the
> [Screen List](screen-list.md), the [Screen Transition Diagram](screen-transition.md),
> [W1](../function-list/w1-function-list.md), the ADRs and the activity diagrams.

## 1. Language and tone

- Interface language: Vietnamese (`vi_VN`, like the client's website). Labels in this repository
  are written in English; every label and message below has its Vietnamese version in the
  translation file. The key labels are seeded in the table at the end of this section.
- Address staff (Receptionist, Nurse, BOD, Admin) as "bạn". Address family members as "quý khách".
- A resident is "người cao tuổi" on staff screens (short form "NCT", as in "Mã NCT"), the term the
  client's website and the reference system use. In text for families, a resident is "cụ" + full
  name ("cụ Nguyễn Văn An"), as the website says "các cụ" and "từng cụ".
- Messages from the nursing home to families speak as "Diên Hồng".
- Button labels are verbs that say what happens: "Update condition", "Save condition",
  "Acknowledge", "Close alert", "Deactivate account", "Assign role". Never "OK", "Submit",
  "Lưu" or "Xác nhận" alone.
- Alert texts are calm and factual: who, where, when, and what is being done.
- Titles and labels are in sentence case. No all-caps titles (the reference system writes
  "HIỆN DIỆN TRONG KHU"; this app writes "Danh sách người cao tuổi").

Key labels:

| English (repository) | Vietnamese (interface) |
|---|---|
| Residents (menu) / Resident list | Người cao tuổi / Danh sách người cao tuổi |
| Chat (menu) / Condition (family menu) | Tin nhắn / Tình trạng |
| Resident ID | Mã NCT |
| New resident | Thêm người cao tuổi |
| Resident profile / Edit profile | Hồ sơ / Sửa hồ sơ |
| Update condition / Save condition | Cập nhật tình trạng / Lưu tình trạng |
| Condition history | Lịch sử tình trạng |
| Message family / Chat with nurse | Nhắn gia đình / Nhắn điều dưỡng |
| Alerts / Acknowledge / Close alert | Cảnh báo / Tiếp nhận cảnh báo / Đóng cảnh báo |
| Real event / False alarm | Sự cố thật / Báo nhầm |
| Report | Báo cáo |
| Accounts / Create account / Assign role / Deactivate account | Tài khoản / Tạo tài khoản / Gán vai trò / Vô hiệu hóa tài khoản |
| Radar status / Logs | Trạng thái radar / Nhật ký |
| Back / Close / Cancel / Back to new record | Quay lại / Đóng / Hủy / Quay lại bản ghi mới |
| Suggestions (under a field) | Gợi ý |
| Search by name or resident ID | Tìm theo tên hoặc mã NCT |

## 2. Formats

| Item | Format | Example |
|---|---|---|
| Date | dd/MM/yyyy | 18/11/2026 |
| Time | HH:mm, 24-hour | 14:32 |
| Date and time | dd/MM/yyyy HH:mm | 18/11/2026 14:32 |
| Short date and time | dd/MM HH:mm, only in a list under a visible month heading | 17/11 14:00 (under "Tháng 11/2026") |
| Period | dd/MM/yyyy – dd/MM/yyyy | 01/11/2026 – 30/11/2026 |
| Duration | m min ss s | 1 min 20 s |
| Phone number | 10 digits in groups 4.3.3 with dots, no country code | 0845.549.996 |
| Room | "Room" + number (Vietnamese: "Phòng") | Room 204 |
| Resident on staff screens | full name · room | Nguyễn Văn An · Room 204 |
| Last condition update | date and time · nurse's name (FR-02-02) | 18/11/2026 08:00 · Lan |
| Row number in a table | No. (Vietnamese "STT"), 1, 2, 3 in the order shown | 3 |
| Counter on a menu item | number; "99+" above 99; hidden at 0 | 2 |
| Alert status | New, Acknowledged, Escalated, Closed, spelled exactly as in AD-UC-06 | Escalated |
| Notice count | "Notice" n "of 3" | Notice 2 of 3 |
| Radar status | Online or Offline, then the time of the last data | Offline · last data 18/11/2026 14:02 |
| Account status | Active or Inactive | Inactive |

The client's website already writes dates as dd/MM/yyyy ("11/03/2025") and phone numbers in
groups with dots ("0845.549.996"), so the app and the website look the same. The reference
system writes "03/08 sáng" in its history list; this app writes the time, never "sáng" or
"chiều", because FR-02-02 stores the time of each record.

## 3. Layout

### 3.1 One app, three widths

One responsive web app for every role, installed on the phone home screen (ADR-001). The layout
changes with the width of the window, never with the role.

| Width | Name | Navigation | Lists | Forms and records |
|---|---|---|---|---|
| 360–767px | Phone | app bar on top, tab bar at the bottom | cards | full screen; primary button fixed at the bottom |
| 768–1023px | Tablet | top bar, sidebar with icons only (64px) | table, scrolls sideways inside its card | record dialog, full width |
| 1024px and wider | Web | top bar, sidebar with icons and labels (240px) | table | record dialog: form on the left, history on the right |

### 3.2 Web app shell (from reference screen 1)

```
+----------------------------------------------------------------------------+
| [=] Diên Hồng                                       Lan · Nurse  v  top bar|
+-------------+--------------------------------------------------------------+
| Residents   | Residents > Resident list                        breadcrumb  |
| Alerts    2 | +----------------------------------------------------------+ |
| Chat      1 | | Resident list                                 [Reload]   | |
|             | | [Room v] [Condition v]         [Search name or ID ][Q]   | |
|   sidebar   | | No. | Resident ID | Full name | Room | Condition | Updated| |
|             | | 1   | ...                                                | |
|             | +----------------------------------------------------------+ |
+-------------+--------------------------------------------------------------+
```

- **Top bar** (56px, colour/surface, bottom edge colour/border): menu button that collapses the
  sidebar, the "Diên Hồng" name, and on the right the account menu with the user's name and role
  (Sign out lives there). The top bar has no counters: each count appears once, on its menu item.
- **Sidebar** (colour/surface, right edge colour/border): one level, only the screens of the user's
  role (3.4). The current screen is on colour/pink-light with colour/primary text and a 3px
  colour/accent bar on its left. The reference system groups items in two levels; this app
  has at most three destinations per role, so it needs one level only. The Alerts item shows the
  number of alerts not acknowledged yet (New and Escalated) and the Chat item the number of unread
  messages; with icons only (64px) the counter sits on the corner of the icon.
- **Content** on colour/background: breadcrumb, then one white page card per screen with the title, the
  toolbar and the content.
- **Toolbar**: filters on the left, quick search on the right ("Search by name or resident ID"
  plus a search button). Actions that belong to one row sit on the row or on the screen they open,
  never in an "Actions" drop-down.

### 3.3 Record dialog (from reference screens 2 and 3)

```
+- Update condition: Nguyễn Văn An · Room 204 -----------------------[x]-+
| * required                         | Condition history   [11/2026 v]  |
| Condition *                        | 18/11 08:00  Stable · Lan        |
| [ Stable                         ] | 17/11 14:00  Fever · Hoa         |
| Suggestions: (Stable) (Fever)      | 17/11 08:00  Stable · Lan        |
| Saved with the time and your name. | View all records                 |
|                [Close] [Save condition]                                |
+------------------------------------------------------------------------+
```

- A record dialog is a **screen** drawn as a large dialog over the list it came from. It has its
  own URL, the browser Back button closes it, and it follows the Screen Transition Diagram (for
  S-F02-02, "taps Back" returns to S-F01-01). It is not the confirm modal of section 4.
- Form on the left (7 of 12 columns), history of the same resident on the right (5 of 12), as in
  the reference. The history is read-only: S-F02-02 shows the last records of S-F02-01 so the
  nurse sees them while entering a new one (UC-04 to UC-05 in the usage flow).
- History per month with a month picker. Selecting a record highlights it with colour/pink-light
  and a colour/primary edge, and shows it read-only in place of the form, with the information
  banner of section 5 and a "Back to new
  record" button. Saved records never change (FR-02-03), so there is no Edit, Copy or Delete on a
  record, and "Save condition" is disabled while a saved record is shown.
- Buttons at the bottom right: one secondary ("Close") then one primary ("Save condition").
- On the phone the same screen is full screen: the form, then the last 3 records, then "View all
  records" to S-F02-01.

### 3.4 Menu per role

| Role | Home after sign in | Menu (web sidebar = phone tab bar) | Usual device (ADR-001) |
|---|---|---|---|
| Receptionist | S-F01-01 Resident list | Residents | computer |
| Nurse | S-F01-01 Resident list | Residents, Alerts (not acknowledged yet), Chat (unread) | phone and computer |
| Residents' Family | S-F04-02 Resident condition | Condition, Alerts, Chat (unread) | phone |
| BOD | S-F05-01 Report | Report | computer |
| Admin | S-F06-01 Account management | Accounts, Radar status, Logs | computer |

A role with one destination has no tab bar on the phone. Hiding a screen from the menu is never
the only check: the API Server checks the role on every request (ADR-003).

### 3.5 Where each screen sits

| Screen | Web (1024px and wider) | Phone (360–767px) |
|---|---|---|
| S-F00-01 Sign in | card 400px wide, centred on colour/background | full screen |
| S-F01-01 Resident list | list page: toolbar + table | search + cards |
| S-F01-02 Resident profile detail | detail page: fields in two columns, actions in the title row | one column, primary button at the bottom |
| S-F01-03 Create or edit resident profile | record dialog, form only | full screen form |
| S-F02-01 Condition history timeline | own page from S-F01-02; also the history panel of S-F02-02 | full screen timeline |
| S-F02-02 Update resident condition | record dialog: form + history | full screen: form, last 3 records |
| S-F03-01 Alert list | list page: table, newest first | cards, newest first |
| S-F03-02 Alert notice and closed notice (family) | column 600px wide, centred | full screen |
| S-F04-01 Nurse chat with family | two panes: conversations, then the thread | conversation list, then the thread |
| S-F04-02 Resident condition (family) | column 600px wide, centred | full screen; resident switcher on top when more than one resident is linked |
| S-F04-03 Chat with nurse | column 600px wide, centred | full screen thread |
| S-F05-01 Report with period filter | filter bar + 3 figure cards | filter bar + stacked figures |
| S-F06-01 Account management | list page: table | cards |
| S-F06-02 Create or edit account | record dialog, form only | full screen form |
| S-F06-03 Assign role to account | record dialog, form only | full screen form |
| S-F06-04 Radar status list | list page: table, Offline rows highlighted (FR-06-10) | cards, Offline cards highlighted |
| S-F06-05 Log list with filters | list page: filter bar + table | filter bar + cards |

### 3.6 What we took from the reference screens

| Reference pattern | In this app | Why |
|---|---|---|
| Dark top bar with counters and the account name | Changed: name and role only, light surface since v3; the counters sit on the Alerts and Chat menu items since v3.1 | the reference's sidebar has no alert item, ours has, so counters in both places showed every count twice; where the menu is hidden (full-screen forms, dialogs) a new alert still arrives as the pop-up (FR-03-02) |
| Dark sidebar, two levels | Changed: one level, the role's screens only, light surface since v3 | at most three destinations per role (3.4); a light shell keeps the 70–20–10 balance of 7.2 |
| Breadcrumb, page title with an icon, reload button | Taken; title in sentence case | |
| Toolbar with a room filter, action drop-downs and quick search | Filters and quick search taken; action drop-downs not taken | actions stay visible on the row or screen they belong to |
| Table with No., ID, name, date of birth, sex, area, room, bed, note | Columns of S-F01-01: No., Resident ID, Full name, Room, Current condition, Last update | date of birth, sex, area and bed are not defined in the resident profile yet (BR-02); add them when the client gives the field list |
| Checkbox on each row | Not taken | no bulk action in W1 |
| Record dialog: form left, history right | Taken for S-F02-02, S-F01-03, S-F06-02, S-F06-03 (3.3) | the nurse sees earlier records while saving a new one |
| Vital-sign fields: blood pressure, glucose, weight, SpO2, pulse, temperature, stool code | Not taken in Release 1 | W1 stores one condition per record (FR-02-02) and does not list its values (AD-UC-05); an open point for the client |
| Required mark "*" in red | Changed: "*" in colour/text-primary and the line "* required" on top of the form | red is kept for resident alerts (section 4) |
| Unit hint under a field ("Đơn vị mmHg") | Taken as the field hint, in colour/text-secondary | a hint in the link colour looks clickable |
| History per month, selected record highlighted yellow with a banner | Taken; the selected record opens read-only, highlighted in colour/pink-light with an information banner | FR-02-03; selected states use the brand's light pink (7.2) |
| Buttons Print, Chart, New, Copy, Save, Delete, Exit | Changed: "Close" and "Save condition" only | Delete and Edit would break FR-02-03; Print and Chart are not in W1; labels say what happens (section 1) |
| Legend box for codes ("X = normal, L = loose...") | Taken as the Legend component for status badges | |
| Text about 12px, light grey labels, white on light teal buttons | Not taken | below 4.5:1 (section 6) |
| Site served over HTTP ("Not secure") | Not taken: HTTPS only | browsers allow installing the app and push notices only on HTTPS (ADR-001, ADR-005) |

The reference system has no phone layout. The phone patterns in 3.1 and 3.5 come from ADR-001
and ADR-005.

## 4. Components

| Component | When to use | Notes |
|---|---|---|
| Top bar | every web and tablet screen | 3.2; menu button, name, account menu; no counters |
| Sidebar | web and tablet | 3.2 and 3.4; counters on the Alerts and Chat items |
| App bar | every phone screen | title of the screen; Back on the left when the screen is not a home screen; account button on the right of a home screen; no counters (the tab bar carries them) |
| Tab bar | phone, roles with more than one destination | 3.4; icon and label on every tab, never an icon alone; counter on the tab; hidden on full-screen forms, where the fixed primary button takes its place |
| Page card | the content of one web screen | colour/surface, colour/border edge, radius 8px, no shadow |
| Toolbar | above a table or a card list | filters left, quick search right |
| Data table | lists on web and tablet | header row on colour/surface-secondary; rows at least 48px tall; the name is a link to the row's screen; row under the pointer on colour/pink-soft, selected row on colour/pink-light |
| Card list item | lists on the phone | full name and room on the first line, status or last update below; the name links to the item's screen; a row action of the table (such as "Update condition") becomes one secondary button on the card |
| Record dialog | create, edit and update screens on web and tablet | 3.3; has its own URL; Esc and Close ask first when there are unsaved changes |
| History panel | right side of S-F02-02; full S-F02-01 | month picker; each record: short date and time, condition, nurse's name |
| Field | every form | label above, field 44px tall with colour/border-strong, hint under it in colour/text-secondary; "*" in colour/text-primary for required fields; a "select or enter" field (AD-UC-05) shows suggestion buttons under it that fill the field |
| Primary button | the one main action of a screen | one per screen, full width and fixed at the bottom on the phone, at least 44px tall |
| Secondary button | alternative actions such as Close, Cancel and Back | outline style |
| Real-time alert pop-up | a new or repeated alert, on every signed-in nurse screen (FR-03-02, FR-03-04) | colour/error header, sound, resident, location and time; one primary button "Acknowledge"; full width on the phone |
| Status badge | the state of an alert, a radar or an account | text AND icon AND colour, never colour alone |
| Legend | next to a list that uses status badges | each badge with its meaning; on colour/surface-secondary |
| Timeline | condition history of one resident (FR-02-04) | records in time order; each shows the date and time and the nurse's name (FR-02-02) |
| Chat bubble | messages between a family and the nurses (UC-09) | own messages on the right, the time under each message |
| Confirm modal | confirm or cancel a single action on one item | Close alert with outcome, Deactivate account, Close without saving; never used for navigation |
| Banner | non-blocking information or an empty state | colour/info-bg, info icon in colour/info, text in colour/text-primary; e.g. "No condition has been recorded yet for cụ Nguyễn Văn An" |
| Inline field error | a field that failed validation (FR-01-01, FR-01-02, FR-02-01, FR-06-04) | under the field, one message per field; colour/warning border and message on colour/warning-bg |
| Toast | short confirmation after success | e.g. "Condition saved" after S-F02-02, or after an account is created, edited or deactivated (`AD-UC-11` S4); white text and white check mark on colour/toast; disappears after 4 seconds |
| Filter bar | period on the report (FR-05-01); user and date on the logs (FR-06-12) | the applied filter stays visible above the list |

Status badges:

| State | Colour token | Icon |
|---|---|---|
| Alert New | colour/error on colour/error-bg | bell |
| Alert Escalated | colour/error on colour/error-bg | bell with "!" and the notice count |
| Alert Acknowledged | colour/pending on colour/pending-bg | person with a check mark |
| Alert Closed | colour/text-secondary on colour/surface-secondary | check mark |
| Radar Online | colour/success on colour/success-bg | dot |
| Radar Offline | colour/warning on colour/warning-bg, row on colour/warning-bg (FR-06-10) | crossed-out signal |
| Account Active | colour/success on colour/success-bg | dot |
| Account Inactive | colour/text-secondary on colour/surface-secondary | lock |

Red (colour/error) is used only for resident alerts and the alert counter. Field errors and the
other error messages (sign-in refused, access denied, network error) use colour/warning, a decision
kept from v1, so a mistyped field never looks like an emergency. Pink never marks a status.

## 5. Messages

| Situation | Pattern | Example |
|---|---|---|
| Sign-in refused (FR-00-01) | what happened + what to do | "The account or password is not correct, or the account is no longer active. Try again or contact the Admin." |
| Access denied (FR-06-03) | what happened + where you are now | "You do not have access to that function. You are back on your home screen." |
| Resident not linked (FR-04-01) | what happened | "You can only see the residents linked to your account." |
| Invalid resident details (FR-01-01, FR-01-02) | field + what to do | "Enter the full name." |
| Condition rejected (FR-02-01) | why + what to do | "The condition is empty. Enter the condition and save again." |
| Condition saved (FR-02-02) | what happened | "Condition saved for Nguyễn Văn An · Room 204." |
| Viewing a saved record (FR-02-03) | what it is + why it cannot change | "Record of 17/11/2026 14:00 by Hoa. Saved records cannot be changed." |
| Close with unsaved changes | consequence | "Close without saving? The condition you entered will be lost." |
| No condition yet (FR-04-02) | what exists | "No condition has been recorded yet for cụ Nguyễn Văn An." |
| No search match | what happened + what to do | "No resident matches “Hùng”. Check the name or the resident ID." |
| New alert, nurse pop-up (FR-03-02) | who + where + when | "Abnormal event: Nguyễn Văn An, Room 204, 14:32." |
| Repeated notice (FR-03-04) | count + what to do | "Not acknowledged yet (notice 2 of 3). Acknowledge it if you are handling it." |
| Notices not allowed on this phone (ADR-005) | what happens + what to do | "Alerts cannot reach this phone yet. Install the app on the home screen and allow notices." |
| First notice to the family (FR-03-09) | what happened + what is being done | "Diên Hồng: an abnormal event was detected for cụ Nguyễn Văn An at 14:32. The nurses have been notified." |
| Closed notice to the family (FR-03-10) | outcome | "Diên Hồng: the alert for cụ Nguyễn Văn An at 14:32 is closed. Outcome: false alarm." |
| Identifier already in use (FR-06-04) | what happened + what to do | "This identifier is already in use. Choose another one." |
| Family account without a resident (FR-06-04) | what to do | "Select at least one resident for a family account." |
| Confirm deactivation (`AD-UC-11` D6) | consequence + no undo | "Deactivate nurse03? This person is signed out at once and can no longer sign in. This cannot be undone." |
| Role outside the permitted scope (`AD-UC-12` S5) | what happened + what to do | "You cannot assign this role. Choose another role." |
| Radar status unavailable (FR-06-11) | what happened, no old data shown | "The radar status cannot be shown right now. Try again later." |
| Network error | what happened + retry | "Not saved yet. Check your connection and try again." |

## 6. Accessibility minimums

- Body text contrast at least 4.5:1 (WCAG 2.2, 1.4.3); icons, badge borders and field borders at
  least 3:1 (1.4.11). Text on every background, the pink selected states included, is checked too (7.6).
- Alert, radar and account states never shown by colour alone (WCAG 2.2, 1.4.1): every state also
  has a text and an icon. Counters carry a text name for screen readers ("2 alerts not acknowledged").
- The alert sound never carries information on its own: the pop-up shows the same resident,
  location and time. The sound stops when the alert is acknowledged and plays for at most
  3 seconds per notice (WCAG 2.2, 1.4.2).
- Targets at least 24 by 24 CSS pixels (WCAG 2.2, 2.5.8); primary buttons and tab bar items at
  least 44px tall.
- Record dialogs and modals keep the keyboard focus inside while open, return it to the element
  that opened them, and close with Esc (asking first when there are unsaved changes).
- Table headers are real header cells (`<th scope="col">`); the link in each row is reachable
  with Tab.
- The fixed primary button on the phone never covers content: the screen has bottom padding equal
  to the button area.
- Every control shows a visible focus ring when reached with the keyboard: 2px colour/primary,
  2px away from the control (WCAG 2.2, 2.4.7).
- Zoom stays allowed: never set `user-scalable=no` or `maximum-scale=1` (WCAG 2.2, 1.4.4).
- Page language set to Vietnamese, `lang="vi"` (WCAG 2.2, 3.1.1).
- Smallest supported width: 360px (ADR-001).

## 7. Design tokens

The tokens are the design system of the app. Their values live in one file,
[design-tokens.css](design-tokens.css). The web app and its phone layout are the same app
(ADR-001) and load the same file, and the UI preview uses it too, so web and phone can never drift
apart. Components use the CSS variables (`var(--colour-primary)`), never a hex value. A token
`group/name` is the CSS variable `--group-name`.

Phone wireframes are drawn at 360px and exported at 3x, so phone images in `screens/img/` are
1080 pixels wide. Web wireframes are drawn at 1280px and exported at 1x.

### 7.1 Colours

Brand identity of Diên Hồng FamilyCare. colour/primary and its hover and pressed shades are darker
than the logo pink, so white text on them passes 4.5:1; the logo pink itself does not (3.2:1).

| Token | Value | Used for |
|---|---|---|
| colour/brand-pink | #F255A1 | logo mark and illustrations only; never text, control edges or states |
| colour/primary | #C21B72 | primary button, links, text and icon of the current menu item and tab, focus ring, selected chip edge |
| colour/primary-hover | #B71B68 | primary button and link under the pointer |
| colour/primary-pressed | #A9145A | primary button and link while pressed |
| colour/secondary | #F191CC | decoration only (illustrations, empty-state art); never text or controls |
| colour/accent | #E61F93 | 3px bar of the current menu item and tab; never text or a filled button |
| colour/pink-light | #FCE7F1 | selected states: current menu item, selected table row, selected history record, selected chip |
| colour/pink-soft | #FFF0F6 | hover of rows, menu items, secondary buttons and chips |
| colour/background | #FFF8FB | page background behind cards, web and phone |
| colour/surface | #FFFFFF | cards, top bar, sidebar, app bar, tab bar, dialogs, fields; text and icons on filled colours |
| colour/surface-secondary | #F8F4F6 | table header, legend, read-only field, loading placeholders, other person's chat bubble |
| colour/border | #E8DEE4 | dividers and card edges (decoration; never the only edge of a control) |
| colour/border-strong | #9B788A | field edges, secondary button and chip edges |
| colour/text-primary | #29232A | titles, body text, table cells, values |
| colour/text-secondary | #6B5863 | labels, hints, timestamps, meta lines, icons of menu items that are not current |
| colour/text-tertiary | #77636F | placeholders, "–" in empty cells, text of disabled fields |
| colour/disabled | #D5CCD1 | disabled primary button (its text colour/text-secondary) |
| colour/success, colour/success-bg | #15803D, #DCFCE7 | Online and Active badges |
| colour/warning, colour/warning-bg | #B45309, #FEF3C7 | field errors and other error messages, Offline radar badge and row |
| colour/error, colour/error-bg | #B91C1C, #FEE2E2 | resident alerts only: alert pop-up header, New and Escalated badges and rows, alert counter |
| colour/info, colour/info-bg | #1D4ED8, #DBEAFE | information banners: a saved record shown read-only, notices not allowed on this phone, empty states |
| colour/pending, colour/pending-bg | #7E22CE, #F3E8FF | Acknowledged alert badge (being handled, outcome still to report) |
| colour/toast | #29232A | toast background, with colour/surface text |
| colour/scrim | #29232A at 55% | behind dialogs and the alert pop-up |
| shadow/dialog | 0 12px 32px #29232A at 18% | dialogs and the alert pop-up only; cards have no shadow |

### 7.2 Colour application (70–20–10)

- About 70% of a screen is neutral: colour/background, colour/surface, colour/surface-secondary,
  text and borders. White space and light backgrounds come first.
- About 20% is colour/pink-light and colour/pink-soft: selected and hover states, highlighted areas.
  Never the background of a whole screen.
- About 10% is colour/primary and colour/accent: the one filled primary button of a screen, links,
  the current menu item and tab.
- Semantic colours keep their meaning and are never replaced by a brand colour: a resident alert is
  always colour/error, never pink, and pink never marks a status.
- No gradients. A shadow only on dialogs. colour/brand-pink, colour/secondary and colour/accent
  never carry text.

### 7.3 Interactive states

| Component | Default | Hover | Pressed | Selected or current | Disabled |
|---|---|---|---|---|---|
| Primary button | colour/primary, colour/surface text | colour/primary-hover | colour/primary-pressed | – | colour/disabled, colour/text-secondary text |
| Secondary button | colour/surface, colour/border-strong edge, colour/text-primary text | colour/pink-soft | colour/pink-light | – | colour/surface-secondary, colour/border edge, colour/text-tertiary text |
| Link | colour/primary | colour/primary-hover, underlined | colour/primary-pressed | – | – |
| Menu item and tab | colour/text-primary label, colour/text-secondary icon | colour/pink-soft | colour/pink-light | colour/pink-light, colour/primary label and icon, 3px colour/accent bar (left in the sidebar, top in the tab bar) | – |
| Table row, card | colour/surface | colour/pink-soft | – | colour/pink-light | – |
| History record | colour/surface | colour/pink-soft | – | colour/pink-light, 1px colour/primary edge | – |
| Suggestion chip | colour/surface, colour/border-strong edge | colour/pink-soft | colour/pink-light | colour/pink-light, colour/primary edge and text | – |
| Field | colour/surface, 1px colour/border-strong | edge colour/text-secondary | – | focus: 2px colour/primary edge | colour/surface-secondary, colour/border edge, colour/text-tertiary text |
| Field with an error | 2px colour/warning edge; message on colour/warning-bg in colour/warning | – | – | – | – |

Focus: every control also shows a 2px colour/primary outline, 2px away from it, when reached with
the keyboard (section 6).

### 7.4 Charts

The report (S-F05-01) shows figures, not charts, in Release 1. When a chart is added: series in
the order colour/primary, colour/info, colour/warning, colour/text-secondary (each at least 3:1 on
white, WCAG 1.4.11); grid lines in colour/border; every series also has a label or its own marker
shape, never colour alone; colour/brand-pink, colour/secondary and colour/accent are not used for
data.

### 7.5 Type, space, size and radius

Unchanged from v2.

| Token | Value | Used for |
|---|---|---|
| font/family | Be Vietnam Pro, fallback Roboto, Arial | all text (full Vietnamese diacritics) |
| font/size | title 22px, section 18px, body 16px, table 15px (web tables only), small 14px, button 16px | line height 1.5 |
| space/unit | 4px; phone screen padding 16px, web content padding 24px, card padding 20px (web) and 16px (phone), list gap 8px | padding, gaps |
| size | top bar and app bar 56px; sidebar 240px (64px with icons only); tab bar 64px; field and button 44px; table row 48px; record dialog up to 1040px wide | |
| radius | primary button 10px, dialog 12px, card and banner 8px, field 6px, badge 999px | corners |
| frame/width | phone 360px, web 1280px | mockups |

### 7.6 Contrast

Checked with the WCAG 2.2 formula:

| Pair | Ratio | Needed |
|---|---|---|
| text-primary #29232A on surface #FFFFFF | 15.4:1 | 4.5:1 (1.4.3) |
| text-primary on background #FFF8FB | 14.7:1 | 4.5:1 (1.4.3) |
| text-primary on pink-light #FCE7F1 | 13.0:1 | 4.5:1 (1.4.3) |
| text-secondary #6B5863 on surface | 6.6:1 | 4.5:1 (1.4.3) |
| text-secondary on surface-secondary #F8F4F6 | 6.0:1 | 4.5:1 (1.4.3) |
| text-secondary on pink-light | 5.6:1 | 4.5:1 (1.4.3) |
| text-tertiary #77636F on surface | 5.5:1 | 4.5:1 (1.4.3) |
| text-tertiary on surface-secondary | 5.1:1 | 4.5:1 (1.4.3) |
| surface on primary #C21B72 | 5.7:1 | 4.5:1 (1.4.3) |
| surface on primary-hover #B71B68 | 6.2:1 | 4.5:1 (1.4.3) |
| surface on primary-pressed #A9145A | 7.2:1 | 4.5:1 (1.4.3) |
| primary on surface (links) | 5.7:1 | 4.5:1 (1.4.3) |
| primary on background | 5.4:1 | 4.5:1 (1.4.3) |
| primary on pink-light (current menu item) | 4.8:1 | 4.5:1 (1.4.3) |
| primary on pink-soft | 5.2:1 | 4.5:1 (1.4.3) |
| success #15803D on success-bg #DCFCE7 | 4.6:1 | 4.5:1 (1.4.3) |
| warning #B45309 on warning-bg #FEF3C7 | 4.5:1 | 4.5:1 (1.4.3) |
| error #B91C1C on error-bg #FEE2E2 | 5.3:1 | 4.5:1 (1.4.3) |
| surface on error (pop-up header, alert counter) | 6.5:1 | 4.5:1 (1.4.3) |
| info #1D4ED8 on info-bg #DBEAFE | 5.5:1 | 4.5:1 (1.4.3) |
| pending #7E22CE on pending-bg #F3E8FF | 5.9:1 | 4.5:1 (1.4.3) |
| surface on toast #29232A | 15.4:1 | 4.5:1 (1.4.3) |
| border-strong #9B788A on surface (field edge) | 3.9:1 | 3:1 (1.4.11) |
| border-strong on background | 3.7:1 | 3:1 (1.4.11) |
| accent #E61F93 on surface (current-item bar) | 4.2:1 | 3:1 (1.4.11) |

Limits that follow from the table: warning on warning-bg (4.51:1) and success on success-bg
(4.57:1) pass with little margin, so neither background may be lightened or the text made smaller
than 14px. colour/brand-pink (3.2:1), colour/accent (4.2:1) and colour/secondary (2.2:1) fail 4.5:1
on white, which is why they never carry text. colour/border (1.3:1) is decoration only: every
control also has a colour/border-strong edge or a label. The disabled button is exempt: WCAG 1.4.3
does not apply to inactive components.

## Change log

| Version | When | Change | Why |
|---|---|---|---|
| v1 | 09/11/2026 | Language, formats, components, messages, accessibility, tokens | First version from the Screen List, W1 and the activity diagrams |
| v2 | 18/11/2026 | Added section 3 (web shell, record dialog, phone layout, menu per role, screen placement, reference screens); new components, messages and tokens; required mark no longer red; website reference changed to dienhongfamilycare.vn | The team chose the reference system's layout; the app needs one convention for the web and the phone (ADR-001) |
| v3 | 18/11/2026 | Colours replaced by the Diên Hồng FamilyCare brand palette; tokens moved to design-tokens.css as the one source for web and phone; light top bar and sidebar; colour application, interactive states and chart rules added (7.2–7.4); Acknowledged badge now colour/pending; information banners now colour/info | The client's brand identity; one token file keeps the web and phone layouts identical (ADR-001) |
| v3.1 | 20/11/2026 | Counters removed from the top bar and the phone app bar; they stay on the Alerts and Chat menu items and tabs | Each count was shown twice on the same screen (top bar and sidebar, app bar and tab bar) |
