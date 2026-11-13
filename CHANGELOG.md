# Changelog

All notable changes to the **RS Islam Al-Hikmah Misfile & Folder Tracking System (`rke517-uts-kj101-02`)** are documented in this file.

---

## [v1.1] - 2026-11-13 (CR-1)

### Changed (Per Client Change Request CR-1)
- **Temporary Folder Merge Escalation Rule (7 Days):** Updated the escalation rule so that unmerged temporary folders (`is_merged = FALSE`) must be merged within **7 days (168 hours)** of issuance; otherwise, an automated escalation alert is sent to the Head of Medical Records.
- **Requirements (`docs/A_requirements.md`):** Updated `R-04` and `R-05` to separate the 3-day missing-folder search escalation from the new **7-day unmerged temporary folder escalation**, and logged CR-1 in Section 3.
- **Analysis Models (`docs/B_models/`):**
  - `Flowmap.md`: Added the 7-day merge deadline decision branch for active temporary folders.
  - `DFD_Level1.md`: Updated Process `4.0 Escalation & Analytics Engine` to audit both `DS-2` (3-day missing folders) and `DS-3` (7-day unmerged temporary folders).
  - `ERD.md`: Added `merge_due_timestamp` (7 days from `issued_timestamp`) to the `TEMPORARY_FOLDER` entity.
  - `Integration_Note.md`: Updated model alignment notes to include the 7-day temporary folder merge audit.
- **Mini-PRD & Build Plan (`docs/PRD.md`, `docs/C_link_table_and_rounds.md`):** Updated Goal, Scope, `US-6`, added acceptance check `C-7 (CR-1)`, added `merge_due_time` to the Data List, and updated Round 2 & Data Link Table.
- **Creative Deliverable (`creative/README.md`):** Updated the "What Changes on Monday" staff infographic (Point 4) to reflect the 7-day temporary folder merge deadline alongside the 3-day missing folder rule.
- **AI Log (`docs/AI_LOG.md`):** Logged AI assistance used for updating CR-1 requirements, diagrams, and PRD.

### What Did NOT Change (and Why)
- **3-Day Escalation for Still-Missing Original Folders:** Unresolved searches where the original folder is still not found remain at **3 days** (per SPO RM-48 and `02_Voice_Note_from_Client.mp3`). *Why:* CR-1 specifically changed the rule for *merging temporary folders* to 7 days, not the search escalation rule for still-missing folders.
- **15-Minute Search Timer Before Issuing Temporary Folders:** Remains **15 minutes** (per SPO RM-48). *Why:* Not requested in CR-1 and essential to prevent patient wait times.
- **Zero-Typing Doctor Status Monitor:** Doctors remain 100% read-only with zero data entry. *Why:* Core constraint from dr. Arif Budiman ("Doctors must not type more than now") remains unchanged.
- **Shelf Misfile Hotspot Tracking & 2-Building Movement:** Shelf-level logging (e.g., Shelf 54) and Building A/B tracking remain unchanged. *Why:* Operational needs from `04_Staff_Chat.png` and `01_Case_Brief_and_Interview.pdf` are unaffected by CR-1.

---

## [v1.0] - 2026-11-11

### Added
- Initial release of Parts A, B, C, E, and F for Case `KJ101-02` (RS Islam Al-Hikmah, Bogor):
  - `docs/A_requirements.md`
  - `docs/B_models/` (`Flowmap.md`, `DFD_Context.md`, `DFD_Level1.md`, `ERD.md`, `Integration_Note.md`)
  - `docs/PRD.md` & `docs/C_link_table_and_rounds.md`
  - `creative/README.md`
  - `docs/AI_LOG.md` & `docs/F_AI_policy_and_reflection.md`
