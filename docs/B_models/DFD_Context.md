# Part B.2: Data Flow Diagram - Context Diagram (Level 0)

**Case Code:** KJ101-02  
**System Name:** RS Islam Al-Hikmah Misfile & Folder Tracking System  

---

## 1. Context Diagram Overview

The Context Diagram defines the boundary of the Medical Record Folder & Misfile Tracking System, identifying its interactions with four key external entities:
1. **Filing Clerk:** Submits search queries, search logs, found locations (including misfile shelf numbers), and executes folder merges. Receives search timers, temp folder issuance prompts, and search status.
2. **Registration Staff:** Requests patient folder availability. Receives temp folder status alerts and ready-for-clinic notifications.
3. **Doctor / Clinic Staff:** Views real-time folder status monitors (read-only, zero typing).
4. **Head of Medical Records:** Receives automated 3-day escalation reports and monthly shelf hotspot analytics.

---

## 2. DFD Context Diagram (Level 0)

```mermaid
graph TD
    FC[Filing Clerk] <-->|Search Logs, Misfile Shelf No, Merge Requests / Timers, Temp Folder Alerts| SYS((0.0 Folder & Misfile Tracking System))
    RS[Registration Staff] <-->|Folder Requests / Temp Folder Notifications| SYS
    DOC[Doctor / Clinic Staff] <-- Read-only Folder Status View -- SYS
    HOD[Head of Medical Records] <-- Escalation Reports & Shelf Hotspot Analytics -- SYS
```

---

## 3. Data Flow Inventory (Context Diagram)

| Flow ID | Source | Target | Data Content |
|---|---|---|---|
| DF-01 | Filing Clerk | System | Missing Folder Search Details (RM No, Patient Name, Initial Shelf, Searcher ID) |
| DF-02 | System | Filing Clerk | Active Search Timer (15-min countdown), Temp Folder Trigger Prompt |
| DF-03 | Filing Clerk | System | Found Location / Misfile Shelf Number (e.g., Shelf 54), Search Resolution |
| DF-04 | System | Registration Staff | Folder Status Alert (`SEARCHING`, `TEMP_ACTIVE`, `READY`) |
| DF-05 | System | Doctor | Live Folder Status Read-Only Display (Queue view, No typing required) |
| DF-06 | System | Head of RM | 3-Day Unresolved Escalation Alert & Monthly Shelf Hotspot Report |
| DF-07 | Filing Clerk | System | Folder Merge Request (Original RM No + Temp Folder ID) |
| DF-08 | System | Filing Clerk | Folder Merge Confirmation & Status Archive |
