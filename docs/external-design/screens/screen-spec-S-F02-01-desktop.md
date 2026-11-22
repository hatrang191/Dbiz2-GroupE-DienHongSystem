# Screen Spec: S-F02-01 Condition history (Desktop)

| Field | Value |
|---|---|
| Screen ID | S-F02-01 |
| Screen name | Condition history |
| Actor | Nurse |
| Priority | Should |
| Feature | F-02 Condition Tracking |
| Activity diagrams | None (`UC-04 View condition history` is marked `not needed` in `usage-flow.md`; related to `AD-UC-05` append-only history rule) |
| Mockup images | `img/S-F02-01-desktop.png` (default), `img/S-F02-01-desktop-numbered.jpg`, five state images (section 2) |
| Frame width | 1280px (exported at 1x) |
| Figma frame | not used (drawn as an HTML wireframe) |
| Status | Done |

## 1. Purpose

**Shown when:** a Nurse selects a resident's condition history from S-F01-01 (Resident list) or clicks "Lịch sử tình trạng" on S-F01-02 (Resident profile detail), or returns here after saving a new condition on S-F02-02 (Update resident condition).

**The user leaves this screen when:** they navigate back via the breadcrumb ("Người cao tuổi" to S-F01-01 or the resident's name to S-F01-02), switch to another section in the sidebar ("Cảnh báo", "Tin nhắn"), click "Nhắn gia đình" (to S-F04-01), or click "Cập nhật tình trạng" (to S-F02-02).

## 2. Mockup

![S-F02-01](img/S-F02-01-desktop.png)

**Numbered:** each number is the # of the element inventory in section 3. Element 8 (Condition history timeline) appears in the default and success states, while element 6 (Error banner) replaces the timeline in the error state (shown on `S-F02-01-desktop-error-numbered.jpg`).

| Default, numbered | Error, numbered |
|---|---|
| ![S-F02-01 numbered](img/S-F02-01-desktop-numbered.png) | ![S-F02-01 error numbered](img/S-F02-01-desktop-error-numbered.png) |

| Loading | Empty |
|---|---|
| ![S-F02-01 desktop loading](img/S-F02-01-desktop-loading.png) | ![S-F02-01 desktop empty](img/S-F02-01-desktop-empty.png) |

| Success |
|---|
| ![S-F02-01 desktop success](img/S-F02-01-desktop-success.png) |

| State | Image |
|---|---|
| Default | `img/S-F02-01-desktop.png` |
| Empty | `img/S-F02-01-desktop-empty.png` |
| Loading | `img/S-F02-01-desktop-loading.png` |
| Error | `img/S-F02-01-desktop-error.png` (network/load failure; access-denied refusal redirects to S-F01-01 per FR-06-03) |
| Success | `img/S-F02-01-desktop-success.png` |

All colours, fonts and corners come from the design tokens in
[ui-conventions.md](../ui-conventions.md#7-design-tokens).

## 3. Element inventory

| # | Element | Type | Content / data source | Required | Validation |
|---|---|---|---|---|---|
| 1 | Sidebar toggle (`[=]`) | Icon button | Static icon (`colour/text-secondary`) in top bar (`56px` height) | Yes | none |
| 2 | Top bar & sidebar navigation | Shell navigation | Brand ("Diên Hồng · Viện dưỡng lão"), signed-in Nurse account menu ("Lan · Điều dưỡng"), and sidebar destinations ("Người cao tuổi" active, "Cảnh báo" with counter, "Tin nhắn" with counter) | Yes | none |
| 3 | Message family (`Nhắn gia đình`) | Secondary button | Static label with chat icon (`1px colour/border-strong`) | Yes | none |
| 4 | Period filter & immutability note | Dropdown + helper text | Label "Thời gian:", month dropdown (`MM/yyyy`, e.g., "Tháng 11/2026"), and static note "Bản ghi đã lưu không thể chỉnh sửa hoặc xóa (FR-02-03)." | Yes | Valid month selection |
| 5 | Breadcrumb | Navigation trail | Path: "Người cao tuổi > " + `Resident Profile.full_name` + " > Lịch sử tình trạng" | Yes | none |
| 6 | Message area (Error / Empty / Toast) | Banner / Toast | Info banner in Empty state ("Chưa có bản ghi tình trạng nào cho cụ [Full Name] trong tháng [MM/yyyy]."); Warning banner with "Thử lại" button in Error state ("Không thể tải lịch sử tình trạng. Kiểm tra kết nối và thử lại."); Toast in Success state ("Đã lưu tình trạng cho [Full Name] · [Room].") | No | none |
| 7 | Update condition (`Cập nhật tình trạng`) | Primary button | Static label with edit icon (`colour/primary`) in page card header | Yes | none |
| 8 | Condition history timeline | Chronological record list | List of `Resident Condition` records sorted newest first: condition text (`condition.value`), timestamp & nurse (`condition.updated_at` · "Điều dưỡng " + `condition.nurse_name`), and "Mới nhất" pill badge (`colour/pink-light`, `colour/primary`) on the top record; no Edit or Delete actions | Yes | formats from `ui-conventions.md` §2 |

## 4. States

| State | What the user sees | Trigger |
|---|---|---|
| Default | Page card titled "Lịch sử tình trạng: [Full Name] · [Room]" with "Nhắn gia đình" and "Cập nhật tình trạng" buttons, month filter ("Tháng 11/2026"), append-only rule note, and chronological list of saved condition records (newest on top with "Mới nhất" badge). | Nurse opens condition history for a resident and records load (FR-02-04) |
| Empty (no data) | Header, action buttons, and month filter remain visible; the record list is replaced by an info banner (`colour/info-bg`) stating "Chưa có bản ghi tình trạng nào cho cụ [Full Name] trong tháng [MM/yyyy]." | No `Resident Condition` records exist for the resident in the selected month |
| Loading | Header, action buttons, and month filter remain visible; the timeline area displays 4 grey skeleton card placeholders (`colour/surface-secondary`). | Condition history records are being fetched from API Server |
| Error | Warning banner (`colour/warning-bg`) displays "Không thể tải lịch sử tình trạng. Kiểm tra kết nối và thử lại." with a "Thử lại" secondary button; record list is hidden. | API request to fetch condition history fails or times out |
| Success / confirmation | Newly saved condition record appears at the top of the timeline highlighted with `colour/pink-light` background, `1px colour/primary` border, and "(Vừa cập nhật)" / "Mới nhất" badge; a dark bottom-right toast (`colour/toast`, auto-dismisses after 4s) confirms "Đã lưu tình trạng cho [Full Name] · [Room]." | Redirected from S-F02-02 after saving a new condition record (FR-02-02, FR-02-03) |

## 5. Interactions and navigation

| # | Element | User action | System response | Goes to screen |
|---|---|---|---|---|
| 1 | Sidebar toggle (`[=]`) | click | Collapses sidebar from 240px to 64px (icons only) or expands it back | stays |
| 2 | Sidebar menu items | click | Opens the selected Nurse destination ("Người cao tuổi", "Cảnh báo", or "Tin nhắn") | S-F01-01 / S-F03-01 / S-F04-01 |
| 3 | Breadcrumb ("Người cao tuổi") | click | Returns to the resident list | S-F01-01 |
| 4 | Breadcrumb (`Resident Profile.full_name`) | click | Returns to the resident's profile detail | S-F01-02 |
| 5 | Month dropdown (`Thời gian`) | select | Filters and reloads condition records for the chosen month | stays (Loading → Default/Empty/Error) |
| 6 | "Nhắn gia đình" button | click | Opens the conversation thread with the resident's linked family | S-F04-01 |
| 7 | "Cập nhật tình trạng" button | click | Opens the Update resident condition record dialog (with history) | S-F02-02 |
| 8 | "Thử lại" button (Error banner) | click (Error state) | Re-fetches the resident's condition history for the selected month | stays (Loading → Default/Empty/Error) |

## 6. Screen-level rules

| Rule ID | Rule | Source |
|---|---|---|
| SR-001 | Only authenticated users with the Nurse role may view condition history; unauthorized requests return to the user's home screen with an access-denied message. | BR-06-01, FR-06-03 |
| SR-002 | Condition records are displayed in reverse chronological order (newest first) showing the condition value, timestamp (`dd/MM/yyyy HH:mm`), and recording nurse's name. | FR-02-02, FR-02-04 |
| SR-003 | Saved condition records are strictly immutable (append-only): no Edit, Copy, or Delete controls are provided on any record in the timeline. | BR-02-01, FR-02-03 |
| SR-004 | Status badges ("Mới nhất") and banners never rely on colour alone; banners pair semantic icons with clear Vietnamese text (`lang="vi"`). | `ui-conventions.md` §4, §6 |

## 7. Linked requirements

| FR ID | What this screen does for it |
|---|---|
| FR-02-02 | Displays the saved timestamp and nurse's name alongside each condition record |
| FR-02-03 | Enforces read-only presentation of historical condition records without overwrite or delete actions |
| FR-02-04 | Lists all condition records of the selected resident in chronological order filtered by month |
| FR-06-03 | Restricts access to the Nurse role and verifies session permissions on every request |

## 8. Responsive and accessibility notes

* Desktop layout (`768px` and wider, drawn at `1280px`) renders S-F02-01 inside the desktop shell with sidebar navigation and a full-width page card; below `768px` (down to `360px`), it switches to a full-screen mobile timeline (`S-F02-01-mobile`) with an app bar and fixed bottom primary button (`ui-conventions.md` §3.1, §3.5).
* Body text contrast is at least `4.5:1` (`colour/text-primary` on `colour/surface` is `15.4:1`; `colour/primary` on `colour/pink-light` is `4.8:1`), and every interactive element shows a `2px` `colour/primary` focus ring (`2px` offset) when navigated by keyboard (`ui-conventions.md` §6, §7.6).
* Information and warning banners combine semantic icons (info circle, warning triangle) with descriptive Vietnamese text (`lang="vi"`).

## 9. Open questions

| # | Question | Blocking? | Status |
|---|---|---|---|
| 1 | [NEEDS CLARIFICATION: Should the period filter also include an "All time" (Tất cả) option in addition to individual months (`MM/yyyy`), or only monthly buckets?] | No | Open. Default: monthly buckets (`Tháng MM/yyyy`) defaulting to the current month per `ui-conventions.md` §3.3. |
| 2 | [NEEDS CLARIFICATION: Should condition records display structured vital-sign fields if added in a future release, or remain a single condition text entry?] | No | Open (`ui-conventions.md` §3.6). Default: single condition value per record in Release 1 per FR-02-02. |

---

## Completion checklist

- [x] The mockup is a separate cropped image file, named with the Screen ID, at the frame width.
- [x] The numbered image exists, and its numbers match the # column of the element inventory.
- [x] Every visible element in the mockup appears in the element inventory.
- [x] Every colour in the mockup is a design token from ui-conventions.md.
- [x] Every input element has a validation rule or an explicit "none".
- [x] All five states are filled in.
- [x] Every navigation target is a Screen ID that exists in the Screen List.
- [x] Every element that displays data names the field it displays.
- [x] Every linked FR exists in the Function List, and every action of this screen is covered by an interaction row.
