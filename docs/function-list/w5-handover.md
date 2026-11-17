# W5 Baseline and handover: Dien Hong System

Lesson 5 (block W5). The baseline every later lesson and DBIZ3 refer to.

## 1. Three scenarios

| Scenario | Person-hours | Cost (VND) | Role in the cash-flow analysis (W6) |
|---|---|---|---|
| Pessimistic: Must only | 139.6 | 39.280.000 | Lowest investment, lowest benefit |
| Base: Must + Should | 197.8 | 55.340.000 | The client figure; base cash flow |
| Optimistic: full scope | 236.0 | 65.600.000 | If the Could pool is never consumed |

## 2. Assumptions

| Assumption | Value | Source |
|---|---|---|
| Junior / Senior / Expert rate | 200.000 / 300.000 / 400.000 VND per hour | Class Parameters (ITviec 2025-26 salary report) |
| AI leverage FE / BE / INT | 0.35 / 0.7 / 1.0 | Class Parameters |
| Verification factor precise / vague | 0.15 / 0.4 | Class Parameters |
| Hours per function point (cross-check only) | 3 | Class Parameters |
| Team capacity | 240 person-hours (4 people x 12 weeks x 5 h) | Class Parameters |
| Money contingency on the Must set | 10% = 3.928.000 VND | Class Parameters |

## 3. tasks.md seed (effective priority Must)

Risk order: 1 = INT (external services), 2 = BE, 3 = FE. DBIZ3 starts with the riskiest rows.

| L3 ID | Layer | Person-hours | Risk order |
|---|---|---|---|
| FR-03-01-INT | INT | 18.4 | 1 |
| FR-03-08-INT | INT | 9.2 | 1 |
| FR-03-09-INT | INT | 11.2 | 1 |
| FR-00-01-BE | BE | 3.4 | 2 |
| FR-01-01-BE | BE | 3.4 | 2 |
| FR-02-01-BE | BE | 3.4 | 2 |
| FR-02-02-BE | BE | 3.4 | 2 |
| FR-02-03-BE | BE | 3.4 | 2 |
| FR-03-01-BE | BE | 3.4 | 2 |
| FR-03-02-BE | BE | 6.8 | 2 |
| FR-03-03-BE | BE | 3.4 | 2 |
| FR-03-04-BE | BE | 3.4 | 2 |
| FR-03-06-BE | BE | 3.4 | 2 |
| FR-03-09-BE | BE | 3.4 | 2 |
| FR-04-01-BE | BE | 3.4 | 2 |
| FR-04-02-BE | BE | 3.4 | 2 |
| FR-06-01-BE | BE | 3.4 | 2 |
| FR-06-02-BE | BE | 3.4 | 2 |
| FR-06-03-BE | BE | 13.6 | 2 |
| FR-06-05-BE | BE | 3.4 | 2 |
| FR-06-07-BE | BE | 3.4 | 2 |
| FR-00-01-FE | FE | 2.0 | 3 |
| FR-01-01-FE | FE | 2.0 | 3 |
| FR-02-02-FE | FE | 2.0 | 3 |
| FR-03-02-FE | FE | 2.0 | 3 |
| FR-03-03-FE | FE | 2.0 | 3 |
| FR-03-06-FE | FE | 2.0 | 3 |
| FR-03-09-FE | FE | 2.0 | 3 |
| FR-04-01-FE | FE | 2.0 | 3 |
| FR-04-02-FE | FE | 2.0 | 3 |
| FR-06-01-FE | FE | 2.0 | 3 |
| FR-06-02-FE | FE | 2.0 | 3 |
| FR-06-05-FE | FE | 2.0 | 3 |
| FR-06-07-FE | FE | 2.0 | 3 |

## 4. Open questions for the client

Collected from the activity diagrams, the ADRs and the business rules. Defaults are what the team builds until the client answers. The detailed answers are in section 5.

Status: **Answered** = settled by an agreed business rule in [W0](w0-scope.md); **Proposed** = team answer, still to confirm with the client (or with the radar vendor where noted).

| # | Question | Blocking? | Owning feature | Default applied | Status |
|---|---|---|---|---|---|
| 1 | Which fields of a resident profile are required, and what makes a detail invalid? (AD-UC-01 Q1, BR-02) | Yes (FR-01-01, FR-01-02) | F-01 | Full name left empty is the invalid case | Proposed |
| 2 | Is the 1-minute resend the same for every severity? (AD-UC-06 Q1) | Yes (FR-03-04) | F-03 | 1 minute for all | Proposed (fits BR-10) |
| 3 | Does "3 notices" include the first notice? (AD-UC-06 Q3) | Yes (FR-03-04, FR-03-05) | F-03 | Yes: the first notice and two more | Answered (BR-10) |
| 4 | After the failure is logged, what happens to the alert, and is anybody told? (AD-UC-06 Q2) | Yes (FR-03-05) | F-03 | The alert stays open on the nurses' list | Partly answered (BR-10); "is anybody told" proposed |
| 5 | If the system is down for a moment, does the radar keep its events and send them later? (AD-UC-06 Q7) | Yes (FR-03-01, FR-03-08) | F-03 | The radar keeps events and resends | Proposed, changes the default; confirm with the radar vendor |
| 6 | Which severity counts as dangerous? The thresholds are set when the radar's AI is trained. (AD-UC-07 Q1, BR-05) | Yes (FR-03-09) | F-03 | Severity High only | Answered (BR-05); definition of High proposed |
| 7 | How long does the system wait between two retries of a failed family push? (AD-UC-07 Q5, BR-09) | Yes (FR-03-11) | F-03 | 1 minute | Answered (BR-09) |
| 8 | Must a nurse be assigned to a resident before exchanging messages with the family? (AD-UC-09 Q2) | Yes (FR-04-03, FR-04-04) | F-04 | Any nurse and any family member can exchange messages | Proposed |
| 9 | After how long without a successful connection check is a radar Offline? (AD-UC-13 Q1, ADR-002) | No | F-06 | 5 minutes | Proposed |
| 10 | How often does the Radar Gateway check each radar's connection? (ADR-002) | No | F-06 | Not decided; must be shorter than the Offline limit | Proposed: every 1 minute |
| 11 | Does the RETINA-4SN answer a status request, or can the gateway only check that it is reachable on the network? (ADR-002) | No | F-06 | Network reachability check | Proposed; confirm with the radar vendor |
| 12 | Should a family member get a push notice for a new chat message when the app is closed? (AD-UC-09) | No | F-04 | No push; messages show when the app is opened | Proposed |
| 13 | Can a room with a radar hold more than one resident? FR-03-01 creates the alert "for the resident in that room". (raised by answer 1) | Yes (FR-03-01, FR-03-09) | F-03 | One resident per room that has a radar | New |
| 14 | Who trains the radar's AI model and labels what counts as High? (raised by answer 6) | Yes (FR-03-01, BR-05) | F-03 | The radar comes with a working model; training is not in this project's hours | New; confirm with the client and the radar vendor |

## 5. Answers to the open questions

Each answer gives the decision, the reasons, and what changes in the other documents if the client accepts it. Facts about the RETINA-4SN and web push come from the sources at the end of this section.

### Q1. Required fields of a resident profile and what makes them invalid

**Answer (proposed).** Four fields are required; every other field is optional.

| Field | Required | Rule | Message when invalid (UI Conventions) |
|---|---|---|---|
| Full name | Yes | Not blank, at most 100 characters, letters (with Vietnamese diacritics) and spaces only | "Enter the full name." |
| Date of birth | Yes | A real date in dd/MM/yyyy, not in the future | "Enter the date of birth as dd/MM/yyyy." |
| Room | Yes | Chosen from the list of rooms, never typed | "Choose the room." |
| Admission date | Yes | A real date in dd/MM/yyyy, not in the future and not before the date of birth | "Enter the admission date as dd/MM/yyyy." |
| Contact phone | No | If entered: 10 digits starting with 0, shown as 4.3.3 | "Enter a 10-digit phone number." |

**Why.**
- The room is required because FR-03-01 finds the resident of an alert through the room of the radar (AD-UC-01 Q2). A resident without a room would make every alert from that room nameless. Choosing from a list removes typing errors such as "204" and "P204".
- The date of birth tells apart residents with the same name, which is common with Vietnamese names.
- The date and phone formats are the ones fixed in the UI Conventions, so every screen shows them the same way.
- The current default (full name empty) stays one of the invalid cases, so the existing tests of AD-UC-01 still hold.

**What changes.** BR-02 gets this field list. FR-01-01 and FR-01-02 keep their wording ("valid", "invalid"). AD-UC-01 Q1 is closed. The answer raises question 13 (shared rooms).

### Q2. Is the 1-minute resend the same for every severity?

**Answer (proposed).** Yes. One wait of 1 minute for every severity in Release 1.

**Why.**
- Acknowledging only says "I am handling it". It takes a few seconds whatever the severity, so a longer wait for a lower severity would only delay the escalation.
- Every alert reaches the nurses, whatever its severity (FR-03-02). The severity is the output of the radar's model and can be wrong: a real fall labelled Medium must not wait longer.
- The harm of a fall grows with the time the person stays on the floor, so the first minutes matter most.
- ADR-004 fixes the wait in the system settings and the Admin cannot change it. One value keeps the Scheduler simple and keeps the BOD's "average time from alert to acknowledgement" (FR-05-01) comparable across alerts.

**What changes.** Nothing; BR-10 already says "within one minute". The team can revisit this after a month of FR-05-01 data if low-severity alerts cause too many escalations.

### Q3. Does "3 notices" include the first notice?

**Answer (agreed, BR-10).** Yes. The first notice and two more, then the failure is logged.

| Time | Event | Alert status | Notice count |
|---|---|---|---|
| 14:32:00 | Alert created, notice 1 | New | 1 |
| 14:33:00 | Nobody acknowledged, notice 2 | Escalated | 2 |
| 14:34:00 | Nobody acknowledged, notice 3 | Escalated | 3 |
| 14:35:00 | Nobody acknowledged, failure logged, no more notices | Escalated | 3 |

**Why.** BR-10 counts the initial notice as one of three. The nurses get three chances within 3 minutes, which keeps the whole escalation short.

**What changes.** AD-UC-06 Q3 is closed. No change to FR-03-04 or FR-03-05.

### Q4. What happens to the alert after the failure is logged, and is anybody told?

**Answer.**
1. **Agreed (BR-10):** the alert stays Escalated and open on every nurse's Alert list (S-F03-01). A nurse can still acknowledge it and close it later; Escalated to Acknowledged is an allowed change in AD-UC-06.
2. **Proposed:** nobody else is notified automatically in Release 1.
3. **Proposed:** the failure is recorded in the Alert Log with the alert and the times of the three notices, so the Admin and the BOD can review it later. Failed family pushes go to the same log (AD-UC-07 Q8).

**Why.** No use case and no FR covers notifying a manager. Doing so needs a new recipient (a head nurse is not an actor in the Use Case Diagram), a new FR and new screens, and FR-03-05 itself is only Could (W4). The base scenario already uses 197.8 of the 240 person-hours.

**Recommendation to the client.** A dangerous alert that nobody acknowledges for 3 minutes is serious. Ask whether a head nurse or the manager on duty should get a phone call in Release 2.

**What changes.** AD-UC-06 Q2 is closed. FR-03-05 can name the Alert Log as the place of the record.

### Q5. Does the radar keep its events while the system is down?

**Answer (proposed; changes the default; confirm with Smart Radar System).** Do not count on the radar. The **Radar Gateway keeps every event until the API Server confirms it**, and forwards it again until then. The gateway restarts automatically after a failure (FR-03-08).

**Why.**
- The public specification of the RETINA-4SN lists a Wi-Fi interface and an update rate of 50 ms. It documents no storage of events on the device and no resend.
- The current default is the risky one: if it is wrong, a fall during an outage is lost without anybody knowing. A gateway that keeps events is safe whether or not the radar resends.
- An outage has two cases. If the API Server is down, the gateway's queue covers it. If the gateway itself is down, events are lost unless the radar resends; FR-03-08 keeps that window short, and the connection checks (FR-06-09) show when it happened.
- An event forwarded late keeps the event time from the radar, so the BOD report (FR-05-01) does not show a false short response time.

**What changes.** ADR-002, job 1: "the gateway stores each event and forwards it again until the API Server confirms it". FR-03-08-INT covers this work. Ask the vendor whether the embedded program can also keep events.

### Q6. Which severity counts as dangerous?

**Answer.**
1. **Agreed (BR-05):** only High.
2. **Proposed definition for labelling:** High = a fall, or a person lying on the floor (not in bed). Lower severities are the other abnormal events, for example leaving the bed at night; they go to the nurses only (FR-03-02), never to the family.

**Why.**
- The RETINA-4SN is sold as a "make your own AI" kit: the buyer collects point clouds, trains a model on a PC and embeds it in the radar. The severity is therefore a label of the trained model, not a factory setting, and "High" has to be defined in words before anybody labels data.
- A fall and lying on the floor are what a family must hear about at once. Notices for smaller events would make families ignore the notices that matter.
- Mistakes will happen: a published study with this radar reports 95% accuracy for fall detection. A fall labelled lower than High still reaches every nurse; only the family notice is skipped.

**What changes.** BR-05 gets the definition of High. ADR-002 notes that the model is trained and embedded by whoever sets up the radar. The answer raises question 14 (who trains the model).

### Q7. How long between two retries of a failed family push?

**Answer (agreed, BR-09).** 1 minute. The first push plus up to 3 retries, then the failure is logged: at most 4 attempts in about 3 minutes.

| Time | Attempt |
|---|---|
| t | First notice (BR-06) |
| t + 1 min | Retry 1 |
| t + 2 min | Retry 2 |
| t + 3 min | Retry 3; if it fails, log the failed push (BR-09) |

**Proposed details.**
- Retry only a failure that can pass: the push service is busy (HTTP 429) or has a temporary error (5xx). A 404 or 410 answer means the family's push subscription is invalid or expired, so a retry cannot succeed: log the failure at once and mark the subscription as gone. The family gets push notices again after opening the web app and allowing notices.
- A retry is the same first notice sent again, not a new notice, so BR-06 ("one first notice") still holds.
- The 1-minute wait is timed by the Scheduler, as for the nurse alerts: the API Server saves "next retry due" on the family notice. ADR-004 currently covers only the alert wait and must be widened.

**What changes.** FR-03-11 adds "1 minute apart" to match BR-09. ADR-004 extends to family retries. AD-UC-07 Q5 is closed.

### Q8. Must a nurse be assigned to a resident before messaging the family?

**Answer (proposed).** No assignment in Release 1.
- Each resident has one conversation with their family, shared by all nurses. Any signed-in nurse can read it and answer.
- A family member can only write about residents linked to their account (BR-12 applies to chat as well).

**Why.**
- W0 has no data on which nurse cares for which resident and no shift data. "The nurse on duty" in FR-04-03 can therefore only mean "the signed-in nurses" today.
- Nurses already see every resident's profile (UC-03), so a shared conversation shows them nothing new.
- At night a few nurses cover all rooms. A shared conversation lets whoever is working answer, instead of a message waiting for one assigned nurse.
- Assignment would need a new data group, a new Admin screen and new FRs, outside the capacity.

**What changes.** FR-04-03 says "the signed-in nurses" instead of "the nurse on duty"; FR-03-02 and FR-03-04 use the same meaning. AD-UC-09 Q2 is closed.

### Q9. After how long is a radar Offline?

**Answer (proposed).** Keep 5 minutes without a successful connection check.

**Why.** A Wi-Fi drop of a minute or two should not mark a radar Offline: false Offline states teach the Admin to ignore the page. 5 minutes is still short compared with a shift.

**Limit to tell the client.** The Admin is not notified when a radar goes Offline (AD-UC-13 Q3), so the real delay is 5 minutes plus the time until the Admin opens S-F06-04. A room with a broken radar has no fall detection at all (ADR-002). Ask whether an Offline radar should notify the Admin or the nurses in Release 2.

**What changes.** Nothing; FR-06-09-BE already uses 5 minutes. AD-UC-13 Q1 is closed.

### Q10. How often does the Radar Gateway check each radar?

**Answer (proposed).** Every 1 minute.

**Why.**
- With an Offline limit of 5 minutes (Q9), a 1-minute interval gives about 5 checks inside the window. One lost check never marks a radar Offline, and a dead radar shows Offline within 5 to 6 minutes.
- One small check per radar per minute is a very light load on the home's network, even with a radar in every room.
- A shorter interval gains little, because the Offline limit stays at 5 minutes.

**What changes.** ADR-002: "fixed interval" becomes 1 minute, kept in the system settings like the values of ADR-004. FR-06-09-INT states the interval.

### Q11. Does the RETINA-4SN answer a status request?

**Answer (proposed; confirm with Smart Radar System).** Release 1 keeps the default: a network reachability check, plus the time of the last data received. Ask the vendor whether the program embedded in the radar can send a heartbeat (for example once a minute). If it can, the gateway uses the heartbeat instead.

**Why.**
- The public specification lists only a Wi-Fi interface, and the kit lets the buyer embed their own program. It documents no status command.
- A reachability check proves that the radar's network part answers, not that its AI is running. ADR-002 names a "frozen" radar as a failure to catch; a frozen program may still answer the network check.
- A heartbeat sent by the embedded program proves the whole chain works: sensor, model and Wi-Fi.

**What changes.** FR-06-09-INT says "connection check or heartbeat", so the work item stays valid with either answer.

### Q12. Should families get a push notice for a new chat message?

**Answer (proposed).** No push for chat messages in Release 1. Families see new messages when they open the web app (S-F04-03).

**Why.**
- The push notice on a family's phone is the channel for dangerous alerts (BR-06). If chat also sends notices, families learn to ignore them, and the one notice that matters no longer stands out.
- FR-04-03 and FR-04-04 do not ask for it, and it is outside the capacity.

**If the client wants it.** It is one more notice type on the existing Notification Service: a new FR at priority Could, with a different title and sound from alert notices.

### Sources

- Smart Radar System, RETINA-4SN Developer Kit product page, a copy of the vendor site hosted on GitHub Pages (Wi-Fi interface, 50 ms update rate, 7 m x 7 m area, train and embed your own AI): https://eunseok0722.github.io/smartradarsystem/en/products/retina_4sn_developer_kit.html
- Ahn et al., "Non-Contact Fall Detection System Using 4D Imaging Radar for Elderly Safety", preprint, 2025 (RETINA-4SN, 95% fall detection accuracy): https://www.preprints.org/manuscript/202504.0809
- web.dev, "Push notifications: common issues" (HTTP status codes 404, 410 and 429 from push services): https://web.dev/articles/push-notifications-common-issues-and-reporting-bugs
