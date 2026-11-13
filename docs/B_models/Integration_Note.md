# Part B.5: Models Integration Note

**Case Code:** KJ101-02  
**Hospital:** RS Islam Al-Hikmah, Bogor  
**Version:** v1.1 (Updated for CR-1 on 13 November 2026)  

---

## How Flowmap, DFD, and ERD Fit Together

The three analytical models created in Part B represent complementary views of the same health information management domain at RS Islam Al-Hikmah:

1. **Flowmap to DFD Alignment:**
   * The **Flowmap** documents the chronological, human-centered operational steps—from the moment a folder is missing on the shelf, through the 15-minute search timer, temporary folder creation, 3-day still-missing escalation, and the **7-day temporary folder merge deadline (CR-1)**.
   * The **DFD (Context & Level 1)** translates these physical operational steps into balanced system processes:
     * Step 1–3 of Flowmap -> **Process 1.0 (Log & Manage Search)**
     * Step 4 of Flowmap -> **Process 2.0 (Issue & Track Temporary Folder)**
     * Step 6–7 of Flowmap -> **Process 3.0 (Execute Folder Merge)** & **Process 4.0 (Escalation & Analytics Engine)**

2. **DFD Data Stores to ERD Alignment:**
   * Every data store in the DFD Level 1 maps directly to one or more primary relational tables in the ERD:
     * `DS-1: Patient_Records` <---> `PATIENT` table
     * `DS-2: Misfile_Search_Logs` <---> `MISFILE_LOG` table (tracks 3-day missing folder escalation)
     * `DS-3: Temporary_Folders` <---> `TEMPORARY_FOLDER` table (tracks `merge_due_timestamp` for 7-day merge escalation per CR-1)
     * `DS-4: Shelf_Hotspot_Analytics` <---> `SHELF_LOCATION` table

3. **Case-Specific Data Item Integration (Staff Chat & CR-1):**
   * Mbak Rini's staff chat (`04_Staff_Chat.png`) identified tracking misfile shelves (such as Shelf 54 for RM `45-61-20`), captured via `found_shelf_id`.
   * **CR-1** added the 7-day merge rule for temporary folders, integrated consistently across the Flowmap (7-day decision), DFD Level 1 (`DS-3` to `Process 4.0`), and ERD (`TEMPORARY_FOLDER.merge_due_timestamp`).
