# Part C.1: Product Requirements Document (Mini-PRD)

**Project Name:** RS Islam Al-Hikmah Misfile & Folder Tracking System  
**Case Code:** KJ101-02  
**Client:** dr. Arif Budiman (Doctor & Member of Medical Committee)  
**Hospital:** RS Islam Al-Hikmah, Bogor  
**Author:** Pradana Ilham Ismail (NIM: 20240306057, Class: KJ101)  
**Target Release:** v1.0 (11 November 2026)  
**Standard Compliance:** RKE517 Week 6 Mini-PRD Standard (6 Parts, One Page)  

---

## 1. Problem and Goal

* **Problem:** At RS Islam Al-Hikmah, Bogor, filing clerks cannot find up to 10 medical record folders on the shelves on busy days. Doctors and patients wait, temporary folders are created after searching but are frequently never merged, creating duplicate records, while paper loan book handwriting is unreadable and files move untracked between two buildings.
* **Goal:** Always know the real-time status and location of every missing folder search, automatically trigger temporary folder creation after 15 minutes, eliminate unmerged temporary folders through guided merging, and track shelf misfile hotspots, with zero extra typing required from doctors.

---

## 2. Users and Scope

* **Users:**
  * **Filing Clerk (Mas Andi / Joko / Mira):** Initiates search logs, tracks 15-minute search timers, issues temporary folders, records misfile shelves, and merges temporary folders.
  * **Registration Staff:** Views folder availability status and receives temporary folder notifications.
  * **Doctor (dr. Arif Budiman):** Views live folder status queue on room display monitor (**100% read-only, zero typing**).
  * **Head of Medical Records:** Receives automated 3-day escalation reports and reviews shelf misfile hotspot analytics.
* **Scope:**
  * **IN:** Search logging, 15-minute search timer, temporary folder ID generation (`TEMP-XXXXXX`), misfile shelf tracking (e.g., Shelf 54), 3-day escalation to Head of RM, guided folder merging, read-only doctor status view, inter-building location tagging.
  * **OUT (Strictly Excluded):** Doctor typing/data entry (doctors benefit but do not type into this system), document scanning, registration, billing, full EHR clinical charting.

---

## 3. User Stories

* **US-1:** As a filing clerk, I want to log every missing folder search with RM number, patient name, and initial shelf, so that I can track active search timers and folder status.
* **US-2:** As a filing clerk, I want the system to alert me when a search exceeds 15 minutes, so that I can issue a temporary folder without keeping the doctor and patient waiting.
* **US-3:** As a filing clerk, I want to record the exact shelf where a misfiled folder was found, so that we can identify which shelves cause the most misfiles.
* **US-4:** As a filing clerk, I want to select an active temporary folder and merge it with the original RM record, so that duplicate files are eliminated and clinical history is consolidated.
* **US-5:** As a doctor, I want to see the real-time status of my clinic's patient folders on a display monitor, so that I know when a file is ready without typing any extra fields or asking staff.
* **US-6:** As the Head of Medical Records, I want the system to automatically flag and report folders missing for more than 3 days, so that I can investigate long-term unresolved files.

---

## 4. Checks (Acceptance Criteria: Situation → Action → Result)

| Check ID | Situation (Given) | Action (When) | Result (Then) |
|---|---|---|---|
| **C-1 (Normal)** | RM `45-61-20` is requested and located on Shelf 45 within 5 minutes. | Clerk marks search as resolved. | Status shows `ON_SHELF / READY` in room display. |
| **C-2 (15-Min Temp)** | Search for RM `45-61-20` reaches 15 minutes without locating original file. | System timer expires and alerts clerk. | System prompts "Issue Temp Folder", assigns `TEMP-456120`, and updates status to `TEMP_ACTIVE`. |
| **C-3 (Shelf Hotspot)** | Misfiled folder `45-61-20` is located on Shelf 54 instead of Shelf 45. | Clerk inputs `Shelf 54` into Found Shelf field. | Status updates to `FOUND`, and Shelf 54 misfile frequency counter increments by 1. |
| **C-4 (What-If: Dup Temp)** | Temporary folder `TEMP-456120` is already active for RM `45-61-20`. | Clerk attempts to create a second temporary folder for the same RM number. | Refused. System displays "TEMP-456120 is already active in Poli Dalam. Action blocked." |
| **C-5 (What-If: Doctor Typing)** | Doctor dr. Arif views Poli Dalam folder status queue on display monitor. | Doctor clicks or attempts to type in status fields. | Display is strictly read-only. No text inputs or cursor edit boxes appear. |
| **C-6 (3-Day Escalation)** | Temporary folder `TEMP-456120` remains unmerged for 72 hours (3 days). | Daily system cron job executes. | Status updates to `ESCALATED_HEAD` and alert appears on Head of RM dashboard. |

---

## 5. Data List

| Field | Meaning | Example | Required? | Rule |
|---|---|---|---|---|
| `rm_number` | Medical record number of the patient | `45-61-20` | Yes | Must follow format `XX-XX-XX` and exist in patient master |
| `patient_name` | Full name of the patient | `Ratna` | Yes | Populated automatically from patient master |
| `searched_by` | Staff member conducting search | `Joko` | Yes | Selected from active filing staff list |
| `initial_shelf` | Shelf where file should be located | `Shelf 45` | Yes | Selected from shelf master table |
| `found_shelf` | Actual shelf where misfiled folder was located | `Shelf 54` | Only when found | Captures shelf misfile hotspot data |
| `temp_folder_id` | Unique identifier for temporary file | `TEMP-456120` | Only when search > 15 mins | Auto-generated by system |
| `status` | Current state of missing folder search | `TEMP_ACTIVE` | Yes | Enum: `SEARCHING`, `FOUND`, `TEMP_ACTIVE`, `MERGED`, `ESCALATED_HEAD` |
| `building_location` | Hospital building where folder currently resides | `Building A` | Yes | Pick from `Building A`, `Building B` |
| `search_start_time` | Timestamp when search began | `02 Nov 2026, 08:00` | Yes | Filled automatically by system |
| `merge_time` | Timestamp when temp and original folders joined | `04 Nov 2026, 09:15` | Only when merged | Must be filled after `search_start_time` |

---

## 6. Open Questions

* **Q1:** Should the 3-day escalation trigger send an automated email/WhatsApp notification to the Head of RM, or display only on the in-app supervisor dashboard?
* **Q2:** When folders move between Building A and Building B, who is responsible for updating the location tag—the filing clerk upon dispatch or the inter-building courier upon receipt?
* **Q3:** Should the shelf misfile hotspot report display real-time daily rankings or aggregated weekly/monthly totals?
