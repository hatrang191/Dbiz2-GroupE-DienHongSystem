# Screen Spec: S-F04-01 Staff-family conversation (Mobile)

| Field | Value | 
| ----- | ----- | 
| Screen ID | S-F04-01 | 
| Screen name | Staff-family conversation | 
| Actor | Nurse | 
| Priority | Should | 
| Feature | F-04 Staff-Family Messaging | 
| Activity diagrams | AD-UC-08 (actions "Open the conversation linked to the resident", "Enter message text", "Send the message") | 
| Mockup images | `img/S-F04-01-mobile.png` (default), `img/S-F04-01-mobile-numbered.png`, five state images (section 2) | 
| Frame width | 360px (exported at 3x, 1080 pixels) | 
| Figma frame | not used (drawn as an HTML wireframe) | 
| Status | Draft | 

## 1. Purpose

**Shown when:** a Nurse taps a resident conversation from the mobile "Tin nhắn" tab, or taps "Nhắn gia đình" from S-F01-01 (Resident list), S-F01-02 (Resident profile detail), or S-F02-01 (Condition history) on a mobile viewport (`360–767px`) to exchange messages with a resident's linked family member (UC-08).

**The user leaves this screen when:** they tap "Hồ sơ" in the family sub-header to inspect the resident's profile (S-F01-02), or tap the Back arrow button (`←`) in the app bar to return to the conversation list / previous screen.

## 2. Mockup

**Numbered:** each number is the # of the element inventory in section 3. Elements 1–3 match across `S-F04-01-mobile-numbered.png`, `S-F04-01-mobile-error-numbered.png`, and `S-F04-01-mobile-success-numbered.png`; element 5 marks the bottom message composer in the default/success states, while element 4 marks the send-failure warning area above the composer in the error state.

| Default, numbered | Error, numbered | Success, numbered | 
| ----- | ----- | ----- | 
|  |  |  | 

| State | Image | 
| ----- | ----- | 
| Default | `img/S-F04-01-mobile.png` | 
| Empty | `img/S-F04-01-mobile-empty.png` | 
| Loading | `img/S-F04-01-mobile-loading.png` | 
| Error | `img/S-F04-01-mobile-error.png` (message send failure, FR-04-01) | 
| Success | `img/S-F04-01-mobile-success.png` | 

All colours, fonts and corners come from the design tokens in
[ui-conventions.md](../ui-conventions.md#7-design-tokens).

## 3. Element inventory

| \# | Element | Type | Content / data source | Required | Validation | 
| ----- | ----- | ----- | ----- | ----- | ----- | 
| 1 | App bar | Mobile top bar | Back arrow button (`←`) on the left + `Resident Profile.full_name` + " · " + `Resident Profile.room` (e.g., "Nguyễn Văn An · Phòng 204") (`56px` height, `colour/surface`, bottom tab bar hidden on full-screen thread view per `ui-conventions.md` §4) | Yes | none | 
| 2 | Family sub-header (`Hồ sơ`) | Context strip + link | Displays linked family contact ("Người thân: " + `family_contact.full_name` + " · " + `phone` in `4.3.3` dot format) on the left and text link "Hồ sơ" (`colour/primary`) on the right | Yes | formats from `ui-conventions.md` §2 | 
| 3 | Message history feed | Chronological chat feed | Scrollable message list sorted oldest to newest (`FR-04-03`): incoming family bubbles on the left (`colour/surface-secondary`) with sender name, relationship, and `HH:mm` timestamp; outgoing nurse bubbles on the right (`colour/pink-light`, `1px colour/border-strong`) with nurse name, role ("Điều dưỡng"), and `HH:mm` timestamp | Yes | formats from `ui-conventions.md` §2 | 
| 4 | Send error banner / Toast feedback | Warning banner / Toast | In Error state, inline warning banner (`colour/warning-bg`) docked directly above the composer stating "Chưa gửi được tin nhắn. Kiểm tra kết nối và thử lại."; in Success state, dark toast (`colour/toast`, auto-dismisses after 4s) above the composer confirming "Đã gửi tin nhắn tới gia đình cụ \[Full Name\]." | No | none | 
| 5 | Docked message composer | Text input + icon submit button | Full-width bottom input bar (`colour/surface`, `1px colour/border` top) containing text input ("Nhập tin nhắn...") and square primary send button (`44x44px`, `colour/primary`) with paper-plane icon | Yes | Non-empty message text required before sending (FR-04-01) | 

## 4. States

| State | What the user sees | Trigger | 
| ----- | ----- | ----- | 
| Default | Full-screen mobile conversation view (`360px` width): app bar with Back arrow and "Nguyễn Văn An · Phòng 204", family sub-header ("Người thân: Nguyễn Thị Lan · 0845.549.996" + "Hồ sơ" link), chronological incoming and outgoing message bubbles, and docked bottom message composer ("Nhập tin nhắn..." + send icon button). | Nurse opens a resident's family conversation thread on mobile (FR-04-01, FR-04-03) | 
| Empty (no data) | App bar, family sub-header, and docked bottom composer remain visible; the message feed displays a top info banner (`colour/info-bg`) stating "Chưa có tin nhắn nào với gia đình cụ \[Full Name\]. Nhập tin nhắn bên dưới để bắt đầu trao đổi." | Selected resident conversation has no prior messages | 
| Loading | App bar, family sub-header, and docked bottom composer remain visible; the message feed displays 3 alternating grey skeleton bubble placeholders (`colour/surface-secondary`). | Conversation message history is being fetched from API Server | 
| Error | Inline warning banner (`colour/warning-bg`) appears directly above the docked composer stating "Chưa gửi được tin nhắn. Kiểm tra kết nối và thử lại."; the unsent draft text remains preserved inside the message input so the Nurse can retry without retyping. | Message delivery fails due to network timeout or API error (FR-04-01) | 
| Success / confirmation | Sent message bubble appears immediately at the bottom right of the feed (`colour/pink-light`) with sender ("Lan · Điều dưỡng") and timestamp (`HH:mm`), the composer input clears, and a dark toast (`colour/toast`, auto-dismisses after 4s) above the composer confirms "Đã gửi tin nhắn tới gia đình cụ \[Full Name\]." | Message is validated, saved, and delivered to the linked family conversation (FR-04-01, FR-04-03) | 

## 5. Interactions and navigation

| \# | Element | User action | System response | Goes to screen | 
| ----- | ----- | ----- | ----- | ----- | 
| 1 | Back button (`←` in app bar) | tap | Closes the thread view and returns to the mobile message thread list or originating screen | S-F01-01 / S-F01-02 / S-F02-01 | 
| 2 | "Hồ sơ" link in family sub-header | tap | Opens the resident's profile detail screen | S-F01-02 | 
| 3 | Message composer input (`Nhập tin nhắn...`) | type | Updates draft message text | stays | 
| 4 | Send icon button (paper-plane) | tap | Validates non-empty message text; sends message to API Server, appends bubble to the conversation history with sender name, role, and timestamp, clears input, and displays confirmation toast (or shows warning banner while preserving draft on failure) | stays (Success or Error state) | 

## 6. Screen-level rules

| Rule ID | Rule | Source | 
| ----- | ----- | ----- | 
| SR-001 | Only authenticated users with the Nurse role may access staff-side family conversations, and each thread is strictly scoped to the resident and their authorized linked family account(s). | BR-04-01, BR-06-01, FR-06-03 | 
| SR-002 | Empty or whitespace-only messages cannot be sent; tapping the send button with empty text does not submit a request. | FR-04-01 | 
| SR-003 | Every sent and received message is persisted and displayed in chronological order (`oldest` at top, `newest` at bottom) with the sender's display name, role/relationship label, and timestamp (`HH:mm`). | FR-04-03 | 
| SR-004 | If sending a message fails due to network or server error, the system displays a warning banner above the composer and retains the drafted text in the input box so the Nurse can resend immediately. | FR-04-01 | 

## 7. Linked requirements

| FR ID | What this screen does for it | 
| ----- | ----- | 
| FR-04-01 | Allows a Nurse on mobile to compose and send text messages to the family linked to a resident | 
| FR-04-03 | Stores and displays the full chronological conversation history between staff and family with sender identity and timestamps | 
| FR-06-03 | Restricts access to authorized Nurse sessions and enforces resident-family conversation boundaries | 

## 8. Responsive and accessibility notes

* Smallest supported width: `360px` (exported at 3x = `1080px`); at `768px` and wider, the screen switches to the desktop two-pane split layout (`S-F04-01-desktop`) with the thread list on the left and conversation pane on the right (`ui-conventions.md` §3.1, §3.5).

* The mobile bottom tab bar is hidden on the full-screen conversation view so the message composer docks cleanly at the bottom (`44x44px` send button touch target), and the scrollable message feed includes matching bottom padding so the latest message bubble is never hidden (`ui-conventions.md` §4, §6).

* Incoming messages and toast confirmations use polite ARIA live regions (`role="status"` / `aria-live="polite"`), all text/bubbles meet at least `4.5:1` contrast, and browser zoom remains enabled (`lang="vi"`, `ui-conventions.md` §6, §7.6).

## 9. Open questions

| \# | Question | Blocking? | Status | 
| ----- | ----- | ----- | ----- | 
| 1 | \[NEEDS CLARIFICATION: Should nurses also be able to attach photos or documents in staff-family conversations, or is messaging strictly text-only in Release 1?\] | No | Open (`AD-UC-08` Q1). Default: text-only messaging in Release 1 per FR-04-01. | 
| 2 | \[NEEDS CLARIFICATION: When a resident has no linked family user account yet (e.g., pending Admin linking in S-F06-02), should the composer be disabled with an explanatory info banner?\] | No | Open. Default: display info banner if no family account is linked and disable the send button until linked. | 

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