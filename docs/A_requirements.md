# Part A: Client Requirements & Problem Understanding

**Course:** RKE517 Analysis and Design of Health Information Systems  
**Case Code:** KJ101-02  
**Client:** dr. Arif Budiman (Doctor & Member of Medical Committee)  
**Hospital:** RS Islam Al-Hikmah, Bogor (Type C General Hospital, 150 beds, ~600 outpatient visits/day, ~120 inpatients/day, 18 medical records staff, 2 buildings)  
**Student:** Pradana Ilham Ismail (NIM: 20240306057, Class: KJ101)  
**Version:** v1.1 (Updated for CR-1 on 13 November 2026)  

---

## 1. Problem Statement & System Goal

### Problem Statement
At RS Islam Al-Hikmah, Bogor, medical record folders are frequently misfiled or missing (~10 folders/day) across two separate hospital buildings, causing doctors and patients to experience critical care delays. Filing clerks currently rely on illegible handwritten paper loan books and physical tracer cards, resulting in temporary folders being issued after 15 minutes of searching that are frequently never merged back into original folders, creating duplicate patient records and recurring misfile incidents.

### System Goal
To design and deploy a zero-friction web/mobile health information tracking system for filing clerks and registration staff to log missing-folder searches, issue temporary folders after 15 minutes, track physical building movements, provide shelf misfile hotspot analytics, auto-escalate still-missing folders after 3 days and unmerged temporary folders after 7 days (CR-1) to the Head of Medical Records, and deliver real-time folder status visibility to doctors without adding any data entry burden to clinical workflows.

---

## 2. Requirements & Verification Checks (R-01 to R-08)

### R-01: Missing Folder Search Logging
* **Requirement Statement:** The system shall allow filing clerks to initiate and log every missing-folder search event with patient details, searching staff ID, initial shelf location, and search timestamp.
* **Verification Check:** 
  * **Situation:** A filing clerk cannot locate medical record folder `45-61-20` on shelf 45.
  * **Action:** The clerk inputs RM No. `45-61-20`, Patient Name `Ratna`, Staff ID `Joko`, and initial search location `Shelf 45` into the system.
  * **Result:** The system creates a new search record with status `SEARCHING`, logs timestamp `02/11 08:00 WIB`, and initiates an automated 15-minute search timer.

### R-02: Temporary Folder Issuance Trigger
* **Requirement Statement:** The system shall automatically trigger an alert to issue a temporary folder when a missing-folder search reaches 15 minutes without resolution, assigning a unique Temporary Folder ID.
* **Verification Check:**
  * **Situation:** Search for RM `45-61-20` has been active for 15 minutes without locating the original file.
  * **Action:** The system evaluates elapsed search time against SPO RM-48 rules and prompts the clerk to create a temporary file.
  * **Result:** The clerk clicks "Issue Temp Folder", and the system generates Temporary Folder ID `TEMP-456120`, sets `merge_due_timestamp` to 7 days later, updates status to `TEMP_ACTIVE`, and notifies registration staff that the patient can proceed to the clinic.

### R-03: Misfile Location & Shelf Hotspot Logging
* **Requirement Statement:** The system shall capture the exact shelf number or location where a misfiled folder is ultimately located to enable shelf-level hotspot analytics.
* **Verification Check:**
  * **Situation:** Staff member Mbak Rini locates misfiled folder `45-61-20` on Shelf 54 instead of Shelf 45.
  * **Action:** Filing clerk inputs `Shelf 54` into the "Found Location" field upon updating the search log.
  * **Result:** System updates the log status to `FOUND`, records `Shelf 54` as the misfile location, and increments the misfile frequency counter for Shelf 54 in the analytics module.

### R-04: Automated 3-Day Escalation for Still-Missing Folders
* **Requirement Statement:** The system shall automatically escalate any missing folder search log where the original folder remains unfound for 3 consecutive days (72 hours) to the Head of Medical Records.
* **Verification Check:**
  * **Situation:** Original folder `45-61-20` has remained unfound since `02/11 08:00 WIB` and current time reaches `05/11 08:00 WIB` (3 days).
  * **Action:** The system cron job executes its daily missing-folder threshold audit.
  * **Result:** The system flags the record as `ESCALATED_HEAD`, sends an automated high-priority alert to the Head of Medical Records dashboard, and includes full search history logs.

### R-05: Temporary Folder Merging Workflow & 7-Day Escalation (Updated for CR-1)
* **Requirement Statement:** The system shall provide a guided folder merging module that pairs temporary folders with original folders, transfers clinical notes, archives the temporary folder ID, and automatically escalates any temporary folder not merged within **7 days (168 hours)** to the Head of Medical Records.
* **Verification Check (Normal Merge):**
  * **Situation:** Original folder `45-61-20` is found on `04/11` after temporary folder `TEMP-456120` was issued on `02/11`.
  * **Action:** Filing clerk Mira selects original RM `45-61-20`, links `TEMP-456120`, verifies physical document consolidation, and clicks "Execute Merge".
  * **Result:** System marks `TEMP-456120` status as `MERGED`, logs merge date `04/11`, updates primary folder status to `ACTIVE`, and clears active temporary folder alerts.
* **Verification Check (CR-1 7-Day Escalation):**
  * **Situation:** Temporary folder `TEMP-456120` was issued on `02/11 08:00 WIB` and remains unmerged (`is_merged = FALSE`) on `09/11 08:00 WIB` (7 days).
  * **Action:** The daily system cron job audits `merge_due_timestamp`.
  * **Result:** System flags `TEMP-456120` as `ESCALATED_MERGE_OVERDUE` and sends an overdue-merge alert to the Head of Medical Records dashboard.

### R-06: Zero-Typing Doctor Status Dashboard
* **Requirement Statement:** The system shall provide a read-only real-time folder status display for clinic doctors that requires zero text input or extra form field interactions.
* **Verification Check:**
  * **Situation:** Dr. Arif Budiman is waiting for patient Ratna's folder in Poli Dalam.
  * **Action:** Dr. Arif views the Poli Dalam queue dashboard on his workstation screen.
  * **Result:** The screen displays `RM 45-61-20 | Ratna | Status: TEMP_ACTIVE (Room 2)` in real time with zero clicks or typing required from Dr. Arif.

### R-07: Inter-Building Movement Tracking
* **Requirement Statement:** The system shall track physical folder transfers between Building A and Building B to maintain location transparency across the hospital campus.
* **Verification Check:**
  * **Situation:** A medical record folder is requested for an inpatient in Building B while stored in Building A.
  * **Action:** Courier scans folder QR/barcode upon dispatch from Building A and receipt at Building B.
  * **Result:** System updates physical location attribute to `Building B - Inpatient Ward 3`, preventing misfile reports in Building A.

### R-08: Analytical Misfile Reporting Dashboard
* **Requirement Statement:** The system shall aggregate search logs to generate visual analytics showing misfile frequency by shelf, average resolution time, and unmerged temporary folder counts.
* **Verification Check:**
  * **Situation:** Medical Records Supervisor opens the monthly quality review tab.
  * **Action:** Supervisor selects date range `01/11/2026 to 10/11/2026` and clicks "Generate Report".
  * **Result:** System displays a bar chart ranking top misfile shelves (e.g., Shelf 54: 14 misfiles), average search time (18.4 mins), and total active unmerged temp folders (3 files).

---

## 3. Open Questions, Contradiction Resolution & CR-1 Update

### Open Question 1: Reporting Threshold Contradiction (Interview vs. Voice Note & SPO RM-48)
* **Discrepancy Description:** In the interview transcript (`01_Case_Brief_and_Interview.pdf`), dr. Arif Budiman initially stated that missing folders are reported to the Head of Medical Records if not found within **1 week**. However, in the subsequent voice note (`02_Voice_Note_from_Client.mp3`) and on the official paper form SPO RM-48 (`03_Current_Paper_Form.jpg`), the policy is explicitly stated as **3 days**.
* **Open Question for Client:** *"Dear dr. Arif, during our meeting you mentioned a 1-week escalation window, but your voice message and the SPO RM-48 printed form specify 3 days. Could you confirm that 3 days (72 hours) is the correct binding operational rule?"*
* **Sensible Proposal:** We configured the still-missing folder escalation trigger to **3 days (72 hours)** per SPO RM-48 and your voice note, while **CR-1 (12 Nov 2026)** clarified that **unmerged temporary folders** must be merged within **7 days** or escalated to the Head of Medical Records.

### Open Question 2: Shelf Hotspot Granularity & Form Input Balance
* **Discrepancy Description:** The current paper form (`03_Current_Paper_Form.jpg`) captures "Where looked" as a single unstructured handwritten line (e.g., "Shelf 45, loan book"). However, Mbak Rini's staff chat (`04_Staff_Chat.png`) requests specific tracking of which individual shelves cause the most misfiles (e.g., Shelf 54).
* **Open Question for Client:** *"Dear dr. Arif & Mas Andi, to support Mbak Rini's request for shelf misfile hotspot analytics without slowing down filing clerks, should we separate the search log into 'Shelves Searched' (quick-select numeric dropdowns) and 'Found Shelf'?"*
* **Sensible Proposal:** We propose a dual-field interface: a fast dropdown/multi-select for shelf numbers (`Shelf 01` to `Shelf 100`) to power automated shelf hotspot reporting, paired with an optional short note field for non-shelf locations (e.g., "Poli Dalam loan book").
