# Part B.1: AS-IS Operational Flowmap

**Case Code:** KJ101-02  
**Hospital:** RS Islam Al-Hikmah, Bogor  

---

## 1. Description of Today's Work Process (AS-IS)

Currently, at RS Islam Al-Hikmah, Bogor, when a patient arrives for an outpatient or inpatient appointment:
1. **Initial Search:** The filing clerk (e.g., Mas Andi or Joko) searches for the patient's medical record folder on its designated shelf in the central archive.
2. **Secondary Check:** If the folder is missing from the shelf, the clerk checks physical tracer cards and the physical paper loan book to see if the file was borrowed by another unit or building.
3. **Nearby Search:** The clerk searches nearby shelves for wrongly filed folders.
4. **Search Decision Point (15 Minutes):**
   - If found within 15 minutes, the folder is delivered to the clinic.
   - If **not found after 15 minutes**, the filing clerk creates a **Temporary Folder** (Form RM-48) so the patient can be examined by the doctor without further delay.
5. **Care Delivery:** The doctor sees the patient using the temporary folder and writes clinical notes in it.
6. **Post-Care & Search Resolution:**
   - When the original folder is eventually located (e.g., days later on Shelf 54), the temporary folder and original folder are supposed to be **joined (merged) by hand**.
   - However, in practice, temporary folders are frequently **never merged**, causing duplicate records to accumulate, lost clinical history, and unresolved missing cases.
7. **Escalation Threshold:** If a missing folder remains unresolved after **3 days** (per SPO RM-48 & voice note correction), it is reported manually to the Head of Medical Records.

---

## 2. Flowmap Diagram (Mermaid & Step-by-Step)

```mermaid
flowchart TD
    A[Patient Arrives / Folder Requested] --> B[Filing Clerk Searches Designated Shelf]
    B --> C{Folder Found?}
    C -- Yes --> D[Deliver Folder to Clinic / Doctor]
    C -- No --> E[Check Physical Tracer Cards & Loan Book]
    E --> F[Search Nearby Shelves & Other Building]
    F --> G{Search Time > 15 Mins?}
    G -- No & Found --> D
    G -- Yes & Still Missing --> H[Create Temporary Folder Form RM-48]
    H --> I[Deliver Temporary Folder to Doctor]
    I --> J[Doctor Examines Patient & Writes Notes]
    J --> K[Patient Departs / Notes Stored in Temp Folder]
    K --> L{Original Folder Found Later?}
    L -- No (After 3 Days) --> M[Report Missing Folder to Head of RM]
    L -- Yes --> N{Staff Hand-Merge Folders?}
    N -- Yes --> O[Folders Merged & Returned to Shelf]
    N -- No / Forgotten --> P[Duplicate Temp Folder Accumulates & Remains Unmerged]
```
