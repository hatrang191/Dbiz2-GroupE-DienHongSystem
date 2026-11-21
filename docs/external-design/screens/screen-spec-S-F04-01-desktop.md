# Screen Spec: S-F04-01 Staff-family conversation (Desktop)

| Field | Value | 
| ----- | ----- | 
| Screen ID | S-F04-01 | 
| Screen name | Staff-family conversation | 
| Actor | Nurse | 
| Priority | Should | 
| Feature | F-04 Staff-Family Messaging | 
| Activity diagrams | AD-UC-08 (actions "Open the conversation linked to the resident", "Enter message text", "Send the message") | 
| Mockup images | `img/S-F04-01-desktop.png` (default), `img/S-F04-01-desktop-numbered.jpg`, five state images (section 2) | 
| Frame width | 1280px (exported at 1x) | 
| Figma frame | not used (drawn as an HTML wireframe) | 
| Status | Draft | 

## 1. Purpose

**Shown when:** a Nurse clicks "Tin nhắn" in the left sidebar navigation, or clicks "Nhắn gia đình" from S-F01-01 (Resident list), S-F01-02 (Resident profile detail), or S-F02-01 (Condition history) on a desktop viewport (`768px` and wider) to exchange messages with a resident's linked family member (UC-08).

**The user leaves this screen when:** they click "Xem hồ sơ" in the thread header to inspect the resident's profile (S-F01-02), or switch to another destination in the left sidebar ("Người cao tuổi" or "Cảnh báo").

## 2. Mockup

**Numbered:** each number is the # of the element inventory in section 3. Elements 1–8 match across `S-F04-01-desktop-numbered.jpg` and `S-F04-01-desktop-error-numbered.jpg`; element 9 points to the message composer bar in the default state and the send-failure warning banner in the error state.

| Default, numbered | Error, numbered | 
| ----- | ----- | 
|  |  | 

| State | Image | 
| ----- | ----- | 
| Default | `img/S-F04-01-desktop.png` | 
| Empty | `img/S-F04-01-desktop-empty.png` | 
| Loading | `img/S-F04-01-desktop-loading.png` | 
| Error | `img/S-F04-01-desktop-error.png` (message send failure, FR-04-01) | 
| Success | `img/S-F04-01-desktop-success.png` | 

All colours, fonts and corners come from the design tokens in
[ui-conventions.md](../ui-conventions.md#7-design-tokens).

## 3. Element inventory

| \# | Element | Type | Content / data source | Required | Validation | 
| ----- | ----- | ----- | ----- | ----- | ----- | 
| 1 | Sidebar toggle (`[=]`) | Icon button | Static icon (`colour/text-secondary`) in top bar (`56px` height) | Yes | none | 
| 2 | Top bar brand | Shell brand mark | Heart icon + "Diên Hồng · Viện dưỡng lão" | Yes | none | 
| 3 | Top bar account menu | User menu | Signed-in Nurse avatar initials ("L"), name, and role ("Lan · Điều dưỡng") | Yes | none | 
| 4 | Sidebar navigation | Left navigation rail | Nurse destinations: "Người cao tuổi", "Cảnh báo" (with red counter badge `2`), and "Tin nhắn" (active pill in `colour/pink-light` with unread message badge `1`) | Yes | none | 
| 5 | Breadcrumb | Page header trail | Current top-level section label "Tin nhắn" | Yes | none | 
| 6 | Thread list pane (`Tin nhắn với gia đình`) | Master list + search input | Left split pane (`320px` width) with heading "Tin nhắn với gia đình", search box ("Tìm theo tên hoặc mã NCT"), and resident conversation items showing `Resident Profile.full_name` + " · " + `Resident Profile.room`, `family_contact.full_name`, latest message preview, and unread pill badge | Yes | none | 
| 7 | Thread header (`Xem hồ sơ`) | Conversation header | Right split pane header displaying selected `Resident Profile.full_name` + " · " + `Resident Profile.room` (e.g., "Nguyễn Văn An · Phòng 204"), linked family contact ("Người thân: " + `family_contact.full_name` + " (" + `relationship` + ") · " + `phone` in `4.3.3` dot format), and text link "Xem hồ sơ" (`colour/primary`) | Yes | formats from `ui-conventions.md` §2 | 
| 8 | Message history pane | Chronological chat feed | Scrollable message list sorted oldest to newest (`FR-04-03`): incoming family bubbles on the left (`colour/surface-secondary`) with sender name, relationship, and `HH:mm` timestamp; outgoing nurse bubbles on the right (`colour/pink-light`, `1px colour/border-strong`) with nurse name, role ("Điều dưỡng"), and `HH:mm` timestamp | Yes | formats from `ui-conventions.md` §2 | 
| 9 | Message composer & send banner | Form input + submit button / Warning banner | Text input ("Nhập tin nhắn gửi gia đình...") + primary button "Gửi tin nhắn" (`colour/primary`); in Error state, displays inline warning banner (`colour/warning-bg`) above composer: "Chưa gửi được tin nhắn. Kiểm tra kết nối và thử lại." | Yes (composer) / No (banner) | Non-empty message text required before sending (FR-04-01) | 

## 4. States

| State | What the user sees | Trigger | 
| ----- | ----- | ----- | 
| Default | Two-pane desktop messaging view inside the Nurse shell: left thread list ("Tin nhắn với gia đình") with search bar and active thread highlighted (`colour/pink-light` with `3px colour/primary` left bar), right conversation pane showing the resident & family header ("Xem hồ sơ" link), chronological message bubbles, and bottom message composer ("Nhập tin nhắn gửi gia đình..." + "Gửi tin nhắn"). | Nurse opens S-F04-01 and selects a resident conversation thread (FR-04-01, FR-04-03) | 
| Empty (no data) | Thread list and thread header remain visible; the message history pane displays a centred info banner (`colour/info-bg`) stating "Chưa có tin nhắn nào với gia đình cụ \[Full Name\]. Nhập tin nhắn bên dưới để bắt đầu trao đổi." | Selected resident conversation has no prior messages | 
| Loading | Search bar, thread header, and message composer remain visible; thread list items and message bubbles are replaced by grey skeleton placeholders (`colour/surface-secondary`). | Conversation list or message history is being fetched from API Server | 
| Error | Warning banner (`colour/warning-bg`) appears directly above the composer stating "Chưa gửi được tin nhắn. Kiểm tra kết nối và thử lại."; the unsent draft text remains preserved inside the message input so the Nurse can retry without retyping. | Message delivery fails due to network timeout or API error (FR-04-01) | 
| Success / confirmation | Sent message bubble appears immediately at the bottom right of the thread (`colour/pink-light`) with sender ("Lan · Điều dưỡng") and timestamp (`HH:mm`), the composer input clears, and a dark bottom-right toast (`colour/toast`, auto-dismisses after 4s) confirms "Đã gửi tin nhắn tới gia đình cụ \[Full Name\]." | Message is validated, saved, and delivered to the linked family conversation (FR-04-01, FR-04-03) | 

## 5. Interactions and navigation

| \# | Element | User action | System response | Goes to screen | 
| ----- | ----- | ----- | ----- | ----- | 
| 1 | Sidebar toggle (`[=]`) | click | Collapses sidebar from 240px to 64px (icons only) or expands it back | stays | 
| 2 | Sidebar menu items ("Người cao tuổi", "Cảnh báo") | click | Opens the selected Nurse destination | S-F01-01 / S-F03-01 | 
| 3 | Thread search input (`Tìm theo tên hoặc mã NCT`) | type | Filters the left thread list by resident full name or Resident ID (`Mã NCT`) | stays | 
| 4 | Conversation item in left thread list | click | Switches the active conversation in the right pane, loads chronological message history, and clears that thread's unread badge | stays (Loading → Default/Empty) | 
| 5 | "Xem hồ sơ" link in thread header | click | Opens the resident's profile detail screen | S-F01-02 | 
| 6 | Message composer input | type | Updates draft message text | stays | 
| 7 | "Gửi tin nhắn" button (or `Enter` key) | click / press | Validates non-empty message text; sends message to API Server, appends bubble to the conversation history with sender name, role, and timestamp, clears input, and displays confirmation toast (or shows warning banner while preserving draft on failure) | stays (Success or Error state) | 

## 6. Screen-level rules

| Rule ID | Rule | Source | 
| ----- | ----- | ----- | 
| SR-001 | Only authenticated users with the Nurse role may access staff-side family conversations, and each thread is strictly scoped to the resident and their authorized linked family account(s). | BR-04-01, BR-06-01, FR-06-03 | 
| SR-002 | Empty or whitespace-only messages cannot be sent; clicking "Gửi tin nhắn" with empty text does not submit a request. | FR-04-01 | 
| SR-003 | Every sent and received message is persisted and displayed in chronological order (`oldest` at top, `newest` at bottom) with the sender's display name, role/relationship label, and timestamp (`HH:mm`). | FR-04-03 | 
| SR-004 | If sending a message fails due to network or server error, the system displays a clear warning banner and retains the drafted text in the input box so the Nurse can resend immediately. | FR-04-01 | 

## 7. Linked requirements

| FR ID | What this screen does for it | 
| ----- | ----- | 
| FR-04-01 | Allows a Nurse to compose and send text messages to the family linked to a resident | 
| FR-04-03 | Stores and displays the full chronological conversation history between staff and family with sender identity and timestamps | 
| FR-06-03 | Restricts access to authorized Nurse sessions and enforces resident-family conversation boundaries | 

## 8. Responsive and accessibility notes

* Desktop layout (`768px` and wider, drawn at `1280px`) renders S-F04-01 as a two-pane split card (`320px` thread list on the left, flexible chat thread on the right) inside the desktop shell; below `768px` (down to `360px`), it switches to a single-pane mobile conversation view (`S-F04-01-mobile`) with an app bar Back button and docked bottom composer (`ui-conventions.md` §3.1, §3.5).

* Incoming messages and toast confirmations use polite ARIA live regions (`role="status"` / `aria-live="polite"`) so screen readers announce new messages and delivery confirmations without interrupting typing (`ui-conventions.md` §6).

* All text and message bubbles meet at least `4.5:1` contrast (`colour/text-primary` on `colour/pink-light` is `13.8:1`; `colour/text-primary` on `colour/surface-secondary` is `14.5:1`), and every interactive control shows a `2px` `colour/primary` focus ring (`2px` offset) (`lang="vi"`, `ui-conventions.md` §6, §7.6).

## 9. Open questions

| \# | Question | Blocking? | Status | 
| ----- | ----- | ----- | ----- | 
| 1 | \[NEEDS CLARIFICATION: Should nurses also be able to attach photos or documents in staff-family conversations, or is messaging strictly text-only in Release 1?\] | No | Open (`AD-UC-08` Q1). Default: text-only messaging in Release 1 per FR-04-01. | 
| 2 | \[NEEDS CLARIFICATION: When a resident has no linked family user account yet (e.g., pending Admin linking in S-F06-02), should the composer be disabled with an explanatory info banner?\] | No | Open. Default: display info banner if no family account is linked and disable "Gửi tin nhắn" until linked. | 

## Completion checklist

* \[x\] The mockup is a separate cropped image file, named with the Screen ID, at the frame width.

* \[x\] The numbered image exists, and its numbers match the # column of the element inventory.

* \[x\] Every visible element in the mockup appears in the element inventory.

* \[x\] Every colour in the mockup is a design token from ui-conventions.md.

* \[x\] Every input element has a validation rule or an explicit "none".

* \[x\] All five states are filled in.

* \[x\] Every navigation target is a Screen ID that exists in the Screen List.

* \[x\] Every element that displays data names the field it displays.

* \[x\] Every linked FR exists in the Function List, and every action of this screen in AD-UC-08 is covered by an interaction row.