# Screen Spec: S-F03-01 Fall alert list (Mobile)

| Field | Value | 
| ----- | ----- | 
| Screen ID | S-F03-01 | 
| Screen name | Fall alert list | 
| Actor | Nurse | 
| Priority | Must | 
| Feature | F-03 Fall Alert Management | 
| Activity diagrams | AD-UC-06 (actions "Receive and display real-time fall alert", "Show repeat reminders until acknowledged"), AD-UC-07 (actions "Review active fall alerts", "Acknowledge alert", "Close alert after intervention") | 
| Mockup images | `img/S-F03-01-mobile.png` (default), `img/S-F03-01-mobile-numbered.png`, five state images (section 2) | 
| Frame width | 360px (exported at 3x, 1080 pixels) | 
| Figma frame | not used (drawn as an HTML wireframe) | 
| Status | Draft | 

## 1. Purpose

**Shown when:** a Nurse taps the "Cảnh báo" tab in the bottom tab bar (or taps an incoming real-time fall alert notification) on a mobile viewport (`360–767px`) to monitor, acknowledge, or close active fall alerts (UC-06, UC-07).

**The user leaves this screen when:** they tap a resident's name on an alert card to view their profile (S-F01-02), tap "Đóng cảnh báo" to open the Close alert modal (S-F03-02), or switch to another tab in the bottom navigation bar ("Người cao tuổi" or "Tin nhắn").

## 2. Mockup

**Numbered:** each number is the # of the element inventory in section 3. Elements 3 and 4 (Unacknowledged and acknowledged alert cards) appear in the default and success states, while element 6 (Message area) replaces the alert cards in the error and empty states (shown on `S-F03-01-mobile-error-numbered.png`). Element 5 represents the persistent bottom tab bar across all states.

| Default, numbered | Error, numbered | 
| ----- | ----- | 
|  |  | 

| State | Image | 
| ----- | ----- | 
| Default | `img/S-F03-01-mobile.png` | 
| Empty | `img/S-F03-01-mobile-empty.png` | 
| Loading | `img/S-F03-01-mobile-loading.png` | 
| Error | `img/S-F03-01-mobile-error.png` (network/load failure; access-denied refusal redirects to S-F01-01 per FR-06-03) | 
| Success | `img/S-F03-01-mobile-success.png` | 

All colours, fonts and corners come from the design tokens in
[ui-conventions.md](../ui-conventions.md#7-design-tokens).

## 3. Element inventory

| \# | Element | Type | Content / data source | Required | Validation | 
| ----- | ----- | ----- | ----- | ----- | ----- | 
| 1 | App bar | Mobile top bar | Brand heart icon + static title "Cảnh báo" on the left, signed-in Nurse avatar initials ("L") on the right (`56px` height, `colour/surface`, no counters per `ui-conventions.md` §4) | Yes | none | 
| 2 | Status legend card (`Chú giải:`) | Legend panel | Explains the 3 alert status pills with icons: `Mới` ("Chưa tiếp nhận"), `Đã nhắc lại (Lần 2/3)` ("Quá 1 phút chưa tiếp nhận"), and `Đã tiếp nhận` ("Điều dưỡng đang xử lý") | Yes | none | 
| 3 | Unacknowledged fall alert card | Priority alert card | Card with `1px colour/error` border showing `Resident Profile.full_name` + " · " + `Resident Profile.room` (e.g., "Nguyễn Văn An · Phòng 204"), detection timestamp ("Phát hiện lúc " + `alert.detected_at` in `dd/MM/yyyy HH:mm`), status pill (`Mới` or `Đã nhắc lại (Lần 2/3)`), and full-width primary button "Tiếp nhận cảnh báo" (`colour/primary`) | No | formats from `ui-conventions.md` §2 | 
| 4 | Acknowledged fall alert card | Standard alert card | Card with `1px colour/border` showing `Resident Profile.full_name` + " · " + `Resident Profile.room` (e.g., "Phạm Thị Dung · Phòng 205"), detection timestamp ("Phát hiện lúc " + `alert.detected_at`), `Đã tiếp nhận` status pill (`colour/purple-light`), and full-width secondary button "Đóng cảnh báo" (`1px colour/border-strong`) | No | formats from `ui-conventions.md` §2 | 
| 5 | Bottom tab bar | Mobile navigation bar | Three primary Nurse destinations: "Người cao tuổi", "Cảnh báo" (active with `colour/pink-light` fill, `2px colour/primary` top bar, and red unread alert counter badge), and "Tin nhắn" (with unread message counter badge) | Yes | none | 
| 6 | Message area (Error / Empty / Toast) | Banner / Toast | Info banner in Empty state ("Hiện không có cảnh báo nào cần xử lý. Hệ thống radar vẫn đang giám sát liên tục."); Warning banner with "Thử lại" button in Error state ("Không thể tải danh sách cảnh báo. Kiểm tra kết nối và thử lại."); Dark toast above bottom tab bar in Success state ("Đã tiếp nhận cảnh báo của \[Full Name\] · \[Room\].") | No | none | 

## 4. States

| State | What the user sees | Trigger | 
| ----- | ----- | ----- | 
| Default | Mobile app bar ("Cảnh báo"), status legend card (`Chú giải:`), stacked active fall alert cards (unacknowledged cards at top with `colour/error` border and "Tiếp nhận cảnh báo" button, followed by acknowledged cards with "Đóng cảnh báo" button), and bottom tab bar with "Cảnh báo" active and badge count (`2`). | Nurse opens S-F03-01 on mobile and active fall alerts load (FR-03-01, FR-03-02) | 
| Empty (no data) | App bar, status legend card, and bottom tab bar remain visible; the alert cards are replaced by an info banner (`colour/info-bg`) stating "Hiện không có cảnh báo nào cần xử lý. Hệ thống radar vẫn đang giám sát liên tục." | No active (`Mới`, `Đã nhắc lại`, or `Đã tiếp nhận`) `Fall Alert` records exist | 
| Loading | App bar, status legend card, and bottom tab bar remain visible; the alert card list displays 3 grey skeleton card placeholders (`colour/surface-secondary`). | Active fall alert list is being fetched from API Server | 
| Error | Warning banner (`colour/warning-bg`) displays "Không thể tải danh sách cảnh báo. Kiểm tra kết nối và thử lại." with a "Thử lại" secondary button below the status legend card; alert cards are hidden. | API request to fetch active fall alerts fails or times out | 
| Success / confirmation | When a Nurse taps "Tiếp nhận cảnh báo", the card's status pill changes to `Đã tiếp nhận` (`colour/purple-light`), its border returns to neutral `colour/border`, its button changes to "Đóng cảnh báo", and a dark toast (`colour/toast`, auto-dismisses after 4s) above the bottom tab bar confirms "Đã tiếp nhận cảnh báo của \[Full Name\] · \[Room\]." | Nurse acknowledges an active fall alert (FR-03-03) or closes an alert via S-F03-02 (FR-03-04) | 

## 5. Interactions and navigation

| \# | Element | User action | System response | Goes to screen | 
| ----- | ----- | ----- | ----- | ----- | 
| 1 | Resident name / header on alert card | tap | Opens the resident's profile detail screen | S-F01-02 | 
| 2 | "Tiếp nhận cảnh báo" button | tap | Records alert acknowledgement with current timestamp and signed-in Nurse's name (FR-03-03), stops repeat reminders (BR-03-02), updates card status to `Đã tiếp nhận`, switches button to "Đóng cảnh báo", and shows confirmation toast | stays (Success state) | 
| 3 | "Đóng cảnh báo" button | tap | Opens the Close alert confirmation modal with optional resolution note input | S-F03-02 | 
| 4 | "Thử lại" button (Error banner) | tap (Error state) | Re-fetches the active fall alert list from API Server | stays (Loading → Default/Empty/Error) | 
| 5 | Bottom tab bar items ("Người cao tuổi", "Tin nhắn") | tap | Switches to the selected primary Nurse screen | S-F01-01 / S-F04-01 | 

## 6. Screen-level rules

| Rule ID | Rule | Source | 
| ----- | ----- | ----- | 
| SR-001 | Only authenticated users with the Nurse role may view and manage fall alerts; unauthorized requests redirect to the user's home screen with an access-denied message. | BR-06-01, FR-06-03 | 
| SR-002 | Incoming fall alerts from the Radar Gateway are displayed in real time with the resident's full name, room number, detection timestamp (`dd/MM/yyyy HH:mm`), and current status (`Mới`, `Đã nhắc lại`, or `Đã tiếp nhận`). | BR-03-01, FR-03-01 | 
| SR-003 | Unacknowledged fall alerts (`Mới`) repeat reminder notifications every 1 minute up to 3 times (`Đã nhắc lại (Lần 1/3)` to `(Lần 3/3)`) until acknowledged by a Nurse. | BR-03-02, FR-03-02 | 
| SR-004 | Acknowledging an alert records the acknowledgement timestamp and the signed-in Nurse's name, halts repeat reminders, and enables the "Đóng cảnh báo" action so the alert can only be closed after acknowledgement (BR-03-03). | BR-03-02, BR-03-03, FR-03-03 | 
| SR-005 | Alert status pills never rely on colour alone: `Mới` and `Đã nhắc lại` pair an alert bell icon with `colour/error` text on `colour/error-bg`, while `Đã tiếp nhận` pairs a user-check icon with `colour/purple` text on `colour/purple-light` (`ui-conventions.md` §4, §7.6). | `ui-conventions.md` §4 | 

## 7. Linked requirements

| FR ID | What this screen does for it | 
| ----- | ----- | 
| FR-03-01 | Receives and displays active fall alerts in real time on mobile with resident name, room, detection timestamp, and status | 
| FR-03-02 | Displays repeat reminder status (`Đã nhắc lại (Lần X/3)`) every 1 minute up to 3 times while unacknowledged | 
| FR-03-03 | Allows a Nurse to acknowledge an active alert via "Tiếp nhận cảnh báo", recording timestamp and nurse name and stopping repeat reminders | 
| FR-03-04 | Provides the "Đóng cảnh báo" action on acknowledged alerts to launch S-F03-02 for closing the alert | 
| FR-06-03 | Restricts fall alert access and actions to the Nurse role and verifies session permissions | 

## 8. Responsive and accessibility notes

* Smallest supported width: `360px` (exported at 3x = `1080px`); at `768px` and wider, the screen switches to the desktop layout (`S-F03-01-desktop`) with sidebar navigation and a 6-column table (`ui-conventions.md` §3.1, §3.5).

* The scrollable alert list includes bottom padding equal to the bottom tab bar height so the last alert card and its "Đóng cảnh báo" button are never obscured (`ui-conventions.md` §6).

* All card action buttons ("Tiếp nhận cảnh báo", "Đóng cảnh báo") and bottom navigation tabs meet the `44px` minimum touch target height (`24x24px` absolute minimum), and browser zoom remains enabled (`lang="vi"`, `ui-conventions.md` §6).

* Real-time alert updates and toast confirmations use ARIA live regions (`role="status"` / `aria-live="assertive"`), and all text/badges meet at least `4.5:1` contrast (`ui-conventions.md` §6, §7.6).

## 9. Open questions

| \# | Question | Blocking? | Status | 
| ----- | ----- | ----- | ----- | 
| 1 | $$ NEEDS CLARIFICATION: Should closed fall alerts remain viewable in a separate historical tab/filter on S-F03-01, or are only active (`Mới`, `Đã nhắc lại`, `Đã tiếp nhận`) alerts shown here in Release 1? $$ | No | Open (`AD-UC-07` Q1). Default: show active alerts (`Mới`, `Đã nhắc lại`, `Đã tiếp nhận`) in S-F03-01; closed alerts are removed from the active queue once closed in S-F03-02. | 
| 2 | $$ NEEDS CLARIFICATION: When an unacknowledged alert reaches `Đã nhắc lại (Lần 3/3)` without acknowledgement, does the system escalate to a supervisor or remain in `Lần 3/3` state until a Nurse acknowledges it? $$ | No | Open (`AD-UC-06` Q1). Default: remain in `Đã nhắc lại (Lần 3/3)` state in the active alert list until a Nurse taps "Tiếp nhận cảnh báo" per BR-03-02. | 

## Completion checklist

* \[x\] The mockup is a separate cropped image file, named with the Screen ID, at the frame width.

* \[x\] The numbered image exists, and its numbers match the # column of the element inventory.

* \[x\] Every visible element in the mockup appears in the element inventory.

* \[x\] Every colour in the mockup is a design token from ui-conventions.md.

* \[x\] Every input element has a validation rule or an explicit "none".

* \[x\] All five states are filled in.

* \[x\] Every navigation target is a Screen ID that exists in the Screen List.

* \[x\] Every element that displays data names the field it displays.

* \[x\] Every linked FR exists in the Function List, and every action of this screen in AD-UC-06 and AD-UC-07 is covered by an interaction row.