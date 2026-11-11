# Part F.1: AI Use Log (AI_LOG.md)

**Case Code:** KJ101-02  
**Student:** Pradana Ilham Ismail (NIM: 20240306057, Class: KJ101)  

---

## Log of AI Tool Usage

| Date & Time | AI Tool Used | Prompt / Task Description | What Was Kept | What Was Changed or Rejected | Reason for Modification |
|---|---|---|---|---|---|
| **09/11/2026 09:30** | Gemini Task Assistant | "Analyze interview transcript `01` and voice note `02` to extract key operational rules for RS Islam Al-Hikmah." | Extracted the 15-minute search timer, two-building operation, and doctor zero-typing constraint. | Rejected initial AI claim that reporting to Head of RM is 1 week. Corrected to 3 days based on voice note `02` and SPO RM-48 form `03`. | **Mistake Caught:** AI missed the voice note correction where dr. Arif updated the 1-week rule to 3 days. |
| **09/11/2026 14:15** | Gemini Task Assistant | "Generate an ERD schema in Mermaid format for tracking missing medical records and temporary folders." | Entities `PATIENT`, `MISFILE_LOG`, `TEMPORARY_FOLDER`, and `SHELF_LOCATION`. | Added `found_shelf_id` and `total_misfile_count` after analyzing Mbak Rini's staff chat (`04_Staff_Chat.png`). | The initial AI ERD did not include shelf-level misfile hotspot tracking requested by staff in the chat. |
| **10/11/2026 10:00** | Gemini Task Assistant | "Draft functional requirements with Situation -> Action -> Result checks for PRD." | Structure of R-01 through R-08 and Situation-Action-Result format. | Adjusted R-06 to explicitly enforce read-only status display for doctors without any input fields. | Ensuring strict compliance with dr. Arif's rule ("Doctors must not type more than now"). |
| **11/11/2026 11:30** | Gemini Task Assistant | "Create DFD Level 0 Context Diagram and DFD Level 1 for the folder tracking system." | Process decomposition into 1.0 Log Search, 2.0 Issue Temp, 3.0 Merge, and 4.0 Escalations. | Balanced data flows across entities (Filing Clerk, Registration, Doctor, Head) and data stores (DS-1 to DS-4). | Replaced generic process names with case-specific HIS process names aligned with hospital SPO RM-48. |

---

## Detailed Case Mistake Caught & Corrected
* **AI Mistake Description:** During initial analysis, the AI model stated in its draft that unresolved missing folders should be reported to the Head of Medical Records after **1 week**, citing the interview transcript (`01_Case_Brief_and_Interview.pdf`).
* **Human Analyst Correction:** As the human analyst, I cross-referenced all four case files and caught that in `02_Voice_Note_from_Client.mp3`, dr. Arif Budiman explicitly stated: *"I forgot to say one thing in our meeting... it is if not found within 3 days."* This 3-day rule was further corroborated by the printed SPO RM-48 rules on `03_Current_Paper_Form.jpg`. I rejected the AI's 1-week value and updated the requirements, DFD cron job, and PRD to enforce the **3-day (72-hour)** escalation threshold.
