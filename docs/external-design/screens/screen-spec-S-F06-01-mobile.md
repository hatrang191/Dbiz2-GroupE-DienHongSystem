# Screen Spec: S-F06-01 Account management (mobile)

| Field             | Value                                                                                                               |
| ----------------- | ------------------------------------------------------------------------------------------------------------------- |
| Screen ID         | S-F06-01                                                                                                            |
| Screen name       | Account management (interface label: "Danh sách tài khoản" on desktop, "Tài khoản" on mobile)                       |
| Actor             | Admin                                                                                                               |
| Priority          | Must                                                                                                                |
| Feature           | F-06 Administration                                                                                                 |
| Activity diagrams | AD-UC-11 (set up account), AD-UC-12 (assign role-based permissions)                                                 |
| Mockup images     | `img/S-F06-01-mobile.png` (default), two numbered images, four state images and the confirm modal image (section 2) |
| Frame width       | 360px (exported at 3x, 1080 pixels)                                                                                                               |
| Figma frame       | page "BOD & Admin · Mobile 360", frame `S-F06-01-mobile` ([Figma file]())                                           |
| Status            | Done                                                                                                                |

## 1. Purpose

**Shown when:** the Admin has signed in (this is the Admin's home screen, FR-00-01; ui-conventions 3.4), taps "Tài khoản" in the tab bar, or comes back from S-F06-02 or S-F06-03. The Admin finds an account and chooses an operation: create, edit, assign a role or deactivate. Only an Admin reaches this screen; any other user is refused (FR-06-03, section 4).

**The user leaves this screen when:** they start a new account or edit one (S-F06-02), assign a role (S-F06-03), open Radar status (S-F06-04) or Logs (S-F06-05), or sign out.

## 2. Mockup

![S-F06-01 mobile](img/S-F06-01-mobile.png)

**Numbered:** each number is the # of the element inventory in section 3. Elements 16 (Message area) and 17 (Reload) appear only in the error state, so they are numbered on the error image. The "S-F06-01" tag above the title in the mockup is a design annotation, not an element.

| Default, numbered | Error, numbered |
|---|---|
| ![S-F06-01 mobile numbered](img/S-F06-01-mobile-numbered.png) | ![S-F06-01 mobile error numbered](img/S-F06-01-mobile-error-numbered.png) |

| Loading | Empty |
|---|---|
| ![S-F06-01 mobile loading](img/S-F06-01-mobile-loading.png) | ![S-F06-01 mobile empty](img/S-F06-01-mobile-empty.png) |

| Success |
|---|
| ![S-F06-01 mobile success](img/S-F06-01-mobile-success.png) | 

| State   | Image                             |
| ------- | --------------------------------- |
| Default | `img/S-F06-01-mobile.png`         |
| Empty   | `img/S-F06-01-mobile-empty.png`   |
| Loading | `img/S-F06-01-mobile-loading.png` |
| Error   | `img/S-F06-01-mobile-error.png`   |
| Success | `img/S-F06-01-mobile-success.png` |

All colours, fonts and corners come from the design tokens in [ui-conventions.md](../ui-conventions.md#7-design-tokens), whose values live in [design-tokens.css](../design-tokens.css).

## 3. Element inventory

Labels are shown as they appear in the interface (Vietnamese), with the repository label in brackets. 

| # | Element | Type | Content / data source | Required | Validation |
|---|---|---|---|---|---|
| 1 | Title | Header, app bar | static: "Tài khoản" (Accounts) | Yes | none |
| 2 | Account button | Icon button, app bar | initial of the last word of `user.name` (the given name) on colour/pink-light; opens a menu with `user.name`, role name (`user.role`) and "Đăng xuất" (Sign out) | Yes | none |
| 3 | Quick search | Search field | placeholder "Tìm theo tên hoặc tên đăng nhập" (Search by name or username); matches `account.full_name` and `account.identifier` | No | none (SR-005) |
| 4 | Role filter | Dropdown | label "Vai trò" (Role): "Tất cả" (All), "Lễ tân", "Điều dưỡng", "Người nhà", "Ban giám đốc", "Admin" | Yes | one value |
| 5 | Status filter | Dropdown | label "Trạng thái" (Status): "Tất cả" (All), "Đang hoạt động" (Active), "Đã vô hiệu hóa" (Inactive) | Yes | one value |
| 6 | Create account | Primary button | label "Tạo tài khoản" (Create account), full width | Yes | none |
| 7 | Count line | Text | "n tài khoản · m đang hoạt động": n = accounts matching the filters and the search, m = the Active ones among them (SR-009) | Yes | none |
| 8 | Account cards | Card list | one card per account in the User Account & Role data group that matches the filters and the search | Yes | none |
| 9 | Full name | Text, first line of the card | `account.full_name`, plain text in colour/text-primary, not a link (SR-010) | Yes | none |
| 10 | Status badge | Status badge, first line | `account.status`: "Đang hoạt động" (Active, dot icon, colour/success) or "Đã vô hiệu hóa" (Inactive, lock icon, colour/text-secondary) (ui-conventions §4) | Yes | none |
| 11 | Username and role | Text, second line | `account.identifier` + " · " + role name of `account.role` | Yes | none |
| 12 | Edit | Secondary button, third line | label "Sửa" (Edit); accessible name includes the username ("Sửa, nurse03") | Active only | none |
| 13 | Assign role | Secondary button, third line | label "Gán vai trò" (Assign role) (BR-15) | Active only | none |
| 14 | Deactivate account | Secondary button, third line | label "Vô hiệu hóa tài khoản" (Deactivate account); not offered on the signed-in Admin's own card (SR-007) | Active, not own | none |
| 15 | Tab bar | Navigation | "Tài khoản" (current), "Trạng thái radar" (Radar status), "Nhật ký" (Logs), icon and label on every tab (ui-conventions 3.4, §4) | Yes | none |
| 16 | Message area | Banner, under the "Tạo tài khoản" button | the empty message (information banner) and the error message (warning banner) of section 4 | No | none |
| 17 | Reload | Secondary button | label "Tải lại" (Reload), under element 16 in the error state | No | none |

An Inactive account card shows elements 9–11 and the line "Không thể đăng nhập" (Cannot sign in) in colour/text-secondary instead of elements 12–14; right after a deactivation the line reads "Đã vô hiệu hóa lúc dd/MM/yyyy HH:mm · không thể đăng nhập" until the list is reloaded (SR-003).

## 4. States

| State | What the user sees | Trigger |
|---|---|---|
| Default | App bar, search, both filters on "Tất cả", the "Tạo tài khoản" button, count line "24 tài khoản · 22 đang hoạt động" and the account cards, with the tab bar. Active cards show "Sửa", "Gán vai trò" and "Vô hiệu hóa tài khoản" (the signed-in Admin's own card shows no "Vô hiệu hóa tài khoản"). | Screen opened, accounts loaded |
| Empty (no data) | Count line "0 tài khoản", no cards, and the information banner (16): with a search text "Không có tài khoản nào khớp “Hùng”. Kiểm tra tên hoặc tên đăng nhập."; with filters only "Không có tài khoản nào khớp bộ lọc. Đổi vai trò hoặc trạng thái.". Search and filters stay as typed. | No account matches the filters and the search |
| Loading | Search, filters, button and tab bar kept, "Đang tải danh sách tài khoản…" (Loading the account list…) in the place of the count line and three placeholder cards on colour/surface-secondary. | List being fetched (screen opened, Reload, filter or search changed) |
| Error | Warning banner (16) "Chưa tải được danh sách tài khoản. Kiểm tra kết nối và thử lại." and the "Tải lại" button (17); no count line, no cards. | The request to fetch the list failed |
| Success | The card of the deactivated account shows the badge "Đã vô hiệu hóa" and the line "Đã vô hiệu hóa lúc 18/11/2026 14:40 · không thể đăng nhập" instead of buttons 12–14; the count line drops by one active account (mockup: 24 tài khoản · 21 đang hoạt động); the card keeps its position; and the toast "Đã vô hiệu hóa tài khoản nurse03." (Account nurse03 deactivated.) appears above the tab bar for 4 seconds (AD-UC-11 `S4`, FR-06-07). | Deactivation confirmed in the confirm modal and saved |

**Confirm modal** (not drawn, described here only; it is a confirm modal, ui-conventions §4, and answers AD-UC-11 `D6`): title "Vô hiệu hóa tài khoản?" (Deactivate account?), text "Vô hiệu hóa nurse03? Người này bị đăng xuất ngay và không thể đăng nhập lại. Không thể hoàn tác." (ui-conventions §5, Confirm deactivation), buttons stacked: "Vô hiệu hóa tài khoản" (primary, full width) then "Hủy" (Cancel, secondary).

**Situations described in words, not drawn** (Screen & Element List):

- Access denied: a user who is not an Admin and opens this screen is sent back to their own home screen, which shows the message "Bạn không có quyền dùng chức năng đó. Bạn đã được đưa về màn hình chính." (You do not have access to that function. You are back on your home screen.) (FR-06-03, ui-conventions §5). This screen is not shown to that user and is never shown with this message.
- Deactivation fails because of the network: the modal closes, the account stays Active, and the message area (23 on desktop, 16 on mobile) shows, on colour/warning-bg, "Chưa lưu được. Kiểm tra kết nối và thử lại." (new; Not saved yet. Check your connection and try again.).

## 5. Interactions and navigation

| # | Element | User action | System response | Goes to screen |
|---|---|---|---|---|
| 1 | Create account (6) | tap | Opens the account form for a new account (AD-UC-11 `A1` [Create]) | S-F06-02 |
| 2 | Edit (12) | tap | Opens the account form with this account (AD-UC-11 `A4`) | S-F06-02 |
| 3 | Assign role (13) | tap | Opens the role assignment for this account (AD-UC-12 `A1`, "taps Assign role") | S-F06-03 |
| 4 | Deactivate account (14) | tap | Opens the confirm modal for this account (AD-UC-11 `A5`) | stays (modal) |
| 5 | "Vô hiệu hóa tài khoản" in the confirm modal | tap | Sets the account Inactive, ends its open sessions, records the action (FR-06-07, FR-06-08); Success state | stays |
| 6 | "Hủy" in the confirm modal | tap | Closes the modal; nothing is deactivated (AD-UC-11 `D6` [No]) | stays |
| 7 | Quick search (3) | type, or the search key of the keyboard | Filters the cards when the Admin pauses typing or presses the search key (SR-005); Loading, then Default or Empty | stays |
| 8 | Role filter (4), Status filter (5) | choose a value | Filters the cards at once; element 7 updates | stays |
| 9 | Reload (17) | tap | Fetches the list again (Loading, then Default or Error) | stays |
| 10 | "Trạng thái radar" in the tab bar (15) | tap | "taps Radar status in the menu" | S-F06-04 |
| 11 | "Nhật ký" in the tab bar (15) | tap | "taps Logs in the menu" | S-F06-05 |
| 12 | Account button (2), "Đăng xuất" | tap | Ends the session | S-F00-01 |

## 6. Screen-level rules

| Rule ID | Rule                                                                                                                                                                                                                                                          | Source                                                |
| ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| SR-001  | Edit, Assign role and Deactivate account are offered for Active accounts only; an Inactive account cannot be selected for any operation.                                                                                                                      | AD-UC-11 (`A4`, `A5` "active account"), BR-15         |
| SR-002  | Deactivation always asks for confirmation first; it signs the person out at once and cannot be undone; the account data and history are kept.                                                                                                                 | FR-06-07, AD-UC-11 `D6`                               |
| SR-003  | The list keeps the order returned by the API Server; a row does not move when its account is deactivated. Just after a deactivation the row shows the time of the deactivation instead of "–" (or the "không thể đăng nhập" line) until the list is reloaded. | open question 3, FR-06-07                             |
| SR-004  | Account status is shown by text, icon and colour together, never by colour alone.                                                                                                                                                                             | ui-conventions §4 (Status badge), §6 (WCAG 2.2 1.4.1) |
| SR-005  | The filters and the search work together (all must match). The search trims spaces, ignores capitals and Vietnamese diacritics, and matches any part of the full name or the username.                                                                        | ui-conventions §5                                     |
| SR-006  | Only an Admin may use this screen; the API Server checks the role on every request, hiding an element is never the only check.                                                                                                                                | FR-06-03, BR-13, ADR-003                              |
| SR-007  | The signed-in Admin cannot deactivate their own account, and the API Server refuses to deactivate the last active Admin.                                                                                                                                      | open question 2, FR-06-07                             |
| SR-008  | The username of a deactivated account stays reserved and cannot be used for a new account; an Inactive account is not reactivated.                                                                                                                            | S-F06-02 SR-001, open question 1                      |
| SR-009  | The count line counts the accounts that match the filters and the search, and how many of them are Active; it is recomputed after every deactivation.                                                                                                         | FR-06-07                                              |
| SR-010  | The full name is plain text: this app has no account detail screen, and colour/primary is reserved for links and the current item (ui-conventions §7.1).                                                                                                      | Screen List, ui-conventions §4                        |

## 7. Linked requirements

| FR ID    | What this screen does for it                                                                                      |
| -------- | ----------------------------------------------------------------------------------------------------------------- |
| FR-00-01 | Home screen of the Admin after sign-in                                                                            |
| FR-06-01 | "Tạo tài khoản" starts the creation of an account (S-F06-02)                                                      |
| FR-06-02 | "Gán vai trò" selects the Active account whose role will change (S-F06-03)                                        |
| FR-06-03 | Only the Admin reaches the screen; any other user is sent to their own home screen with the access-denied message |
| FR-06-06 | "Sửa" selects the Active account whose information will change (S-F06-02)                                         |
| FR-06-07 | "Vô hiệu hóa tài khoản" deactivates an Active account after confirmation                                          |
| FR-06-08 | The deactivation is recorded in the action log (no user interface here; listed on S-F06-05)                       |

## 8. Responsive and accessibility notes

- Smallest supported width: 360px; screen padding 16px (ui-conventions 3.1, 7.5). At 360px nothing scrolls sideways: a long name wraps to a second line and the card buttons wrap onto the next line.
- The desktop table becomes one card per account; the row actions become secondary buttons on the card (ui-conventions §4, Card list item).
- Buttons and tab bar items are at least 44px tall (ui-conventions 7.5, §6; the card buttons in the current mockup are about 40px and must be redrawn); the tab bar is 64px; zoom stays allowed.
- Account status is never shown by colour alone (SR-004); text contrast at least 4.5:1 on every background used (ui-conventions 7.6).
- Row actions have accessible names that include the username ("Vô hiệu hóa tài khoản, nurse03").

## 9. Open questions

| #   | Question                                                                                                                                               | Blocking? | Status                                                                                                                                                                              |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------ | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | Can the Admin reactivate an Inactive account?                                                                                                          | No.       | Open. Default (AD-UC-11 open question 5): no; the Admin creates a new account with a new username, and the old username stays reserved.                                             |
| 2   | May an Admin deactivate their own account or the last active Admin?                                                                                    | Yes.      | Open. Default, applied until the client answers: not their own account, and the API Server refuses to deactivate the last active Admin; another Admin's account may be deactivated. |
| 3   | In which order are accounts listed, and is the list paged? The mockup lists 6 of 24 accounts in an order that is neither by name nor by status.        | No.       | Open. Default: the order returned by the API Server, stable; all accounts in one scrollable list; no sorting control and no paging in Release 1.                                    |
| 4   | The messages marked (new) (empty list by filters, load error, toast, network error, loading text, "Không thể đăng nhập") are not in ui-conventions §5. | No.       | Closed. Added to ui-conventions v3.4.                                                         |

## Completion checklist

- [x] The mockup is a separate cropped image file, named with the Screen ID, at the frame width.
- [x] The numbered images exist, and their numbers match the # column of the element inventory.
- [x] Every visible element in the mockup appears in the element inventory. 
- [x] Every colour in the mockup is a design token from ui-conventions.md. 
- [x] Every input element has a validation rule or an explicit "none".
- [x] All five states are filled in. 
- [x] Every navigation target is a Screen ID that exists in the Screen List.
- [x] Every element that displays data names the field it displays.
- [x] Every linked FR exists in the Function List, and every action of this screen in AD-UC-11 and AD-UC-12 is covered by an interaction row.
