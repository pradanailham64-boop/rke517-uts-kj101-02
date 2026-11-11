# Part E: Creative Multimodal Deliverables

**Case Code:** KJ101-02  
**Hospital:** RS Islam Al-Hikmah, Bogor  
**Student:** Pradana Ilham Ismail (NIM: 20240306057, Class: KJ101)  

---

## Selected Creative Pieces
For Part E, two creative deliverables have been produced to communicate the system design to different stakeholder audiences:
1. **Piece 1 (Option 2): App Prototype / UI Mock-ups** (For Filing Clerks & Doctors)
2. **Piece 2 (Option 3): "What Changes on Monday" Infographic Poster** (For Counter & Medical Record Staff)

---

## Piece 1: App Prototype / UI Mock-up (Screen Designs)

### Screen 1: Filing Clerk Search & Misfile Logging Interface
Designed for Mas Andi and filing clerks to quickly initiate searches, track the 15-minute search timer, issue temporary folders, and log misfile shelf numbers.

```
+-----------------------------------------------------------------------------------+
|  RS ISLAM AL-HIKMAH - FOLDER & MISFILE TRACKING SYSTEM                            |
|  Logged in as: Mas Andi (Filing Clerk) | Active Building: Building A              |
+-----------------------------------------------------------------------------------+
|  [ SEARCH MISSING FOLDER ]                                                        |
|  Patient RM No:  [ 45-61-20         ]   Patient Name: [ Ratna               ] |
|  Initial Shelf:  [ Shelf 45         ]   Searched By:  [ Joko                ] |
|  [ Start Search Logging ]                                                         |
+-----------------------------------------------------------------------------------+
|  ACTIVE SEARCHES & TIMERS                                                         |
|  -------------------------------------------------------------------------------  |
|  RM No.     Patient  Start Time   Elapsed Time   Timer Status   Action            |
|  45-61-20   Ratna    08:00 WIB    15:02 Mins     [ EXPIRED! ]   [ Issue Temp ]    |
|  18-02-77   Sutrisno 08:10 WIB    05:18 Mins     [ ACTIVE   ]   [ Log Found  ]    |
+-----------------------------------------------------------------------------------+
|  [ LOG FOUND MISFILE LOCATION ]                                                   |
|  Select RM No: [ 45-61-20 (Ratna)   v ]                                           |
|  Found Location / Misfile Shelf: [ Shelf 54         v ] (e.g. Shelf 54 Hotspot) |
|  [ Mark as Found & Complete ]                                                     |
+-----------------------------------------------------------------------------------+
```

### Screen 2: Doctor Real-Time Folder Status Queue (Zero Typing)
Designed for dr. Arif Budiman and clinic doctors in Poli Dalam. **100% Read-Only, Zero Typing.**

```
+-----------------------------------------------------------------------------------+
|  RS ISLAM AL-HIKMAH - POLI DALAM FOLDER STATUS MONITOR                            |
|  Doctor: dr. Arif Budiman, Sp.PD | Room: Poli Dalam 2 | Live Queue               |
+-----------------------------------------------------------------------------------+
|  PATIENT FOLDER STATUS QUEUE (Auto-Refreshes every 15 secs)                       |
|  -------------------------------------------------------------------------------  |
|  Queue #  RM No.     Patient Name   Status           Location / Note              |
|  01       18-02-77   Sutrisno       [ ON SHELF   ]   Folder Ready in Room         |
|  02       45-61-20   Ratna          [ TEMP ACTIVE]   Temp Folder TEMP-456120 Issued|
|  03       12-34-56   Ahmad          [ SEARCHING  ]   Filing Search In Progress    |
+-----------------------------------------------------------------------------------+
|  * Note: Status updates automatically in real-time. No typing or clicks required.  |
+-----------------------------------------------------------------------------------+
```

---

## Piece 2: "What Changes on Monday" Staff Infographic Poster

### Staff Infographic: Transitioning from Paper SPO RM-48 to Digital Tracking

```
=====================================================================================
                   RS ISLAM AL-HIKMAH - UNIT REKAM MEDIS
                   "WHAT CHANGES ON MONDAY?"
       Digital Missing Folder & Temporary Record Management Guide
=====================================================================================

1. BYE-BYE ILLEGIBLE PAPER LOAN BOOKS!
   * Old Way: Writing loan entries by hand in paper books that get lost or unreadable.
   * Monday Way: One-click digital search logging from any workstation computer.

2. STICK TO THE 15-MINUTE RULE AUTOMATICALLY!
   * Old Way: Guessing how long you searched before making a temporary folder.
   * Monday Way: System automatically counts down 15 minutes and alerts you to issue
     Temporary Folder TEMP-XXXXXX so patients are never kept waiting.

3. LOG MISFILE SHELVES TO FIX HOTSPOTS!
   * Old Way: Searching the same wrong shelves repeatedly without fixing the root cause.
   * Monday Way: Input the exact shelf where you found misfiled folders (e.g. Shelf 54)
     so supervisor can audit problem shelves.

4. AUTOMATED 3-DAY ESCALATION TO HEAD OF RM!
   * Old Way: Forgotten missing files sitting unresolved for weeks.
   * Monday Way: System auto-notifies Head of Medical Records after 3 days (72 hours).

5. EASY DIGITAL MERGING!
   * Old Way: Temporary folders never getting joined to original records.
   * Monday Way: Use the "Merge Folders" tab to pair TEMP-XXXXXX with original RM No.

6. ZERO TYPING FOR DOCTORS!
   * Doctors watch live folder status on clinic queue monitors without typing a single field.
=====================================================================================
```
