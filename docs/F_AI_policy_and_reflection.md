# Part F.2: Personal AI Policy & Reflection

**Student:** Pradana Ilham Ismail (NIM: 20240306057, Class: KJ101)  
**Course:** RKE517 Analysis and Design of Health Information Systems  

---

## 1. Personal AI Policy (5 Rules with Reasons)

1. **Rule 1: Never Paste Real Patient Identifiers or Identifiable Health Data into Commercial AI Prompts.**
   * *Reason:* Real Protected Health Information (PHI) is legally protected under HIPAA and Indonesian PDP (Pelindungan Data Pribadi) laws. Disclosing real patient records to external AI cloud services violates patient privacy and medical confidentiality.
2. **Rule 2: Cross-Reference Every AI-Generated Requirement Against Primary Source Artifacts.**
   * *Reason:* AI models frequently hallucinate generic system features or miss subtle corrections across multiple source files (such as missing the voice note correction from 1 week to 3 days in our case).
3. **Rule 3: Maintain Full Human Ownership Over Architectural & Data Modeling Decisions.**
   * *Reason:* System design models (DFDs, ERDs, PRDs) must reflect the exact real-world operational constraints of the healthcare facility, which AI cannot intuitively understand without human domain validation.
4. **Rule 4: Explicitly Document and Declare All AI Tools Used in Project Deliverables.**
   * *Reason:* Academic and professional integrity requires transparent attribution of AI assistance to distinguish automated drafting support from human analytical reasoning.
5. **Rule 5: Use AI as a Collaborative Design Partner, Not a Final Decision Maker.**
   * *Reason:* In Health Information Systems, an unverified AI recommendation implemented in hospital software can cause clinical care delays, duplicate records, or medical errors on real patients.

---

## 2. Reflection: AI in Health Information Systems Design

### Where AI Helped Most
AI served as an exceptionally efficient accelerator during the initial synthesis and formatting phases of system design. It helped rapidly translate unstructured meeting transcripts, paper form images, and staff chats into structured Markdown tables, Mermaid diagram syntax, and standardized PRD sections. Tasks that would typically require hours of repetitive formatting—such as generating Situation-Action-Result test checks, writing draft ERD schemas, and structuring Data Link Tables—were completed in minutes, allowing me to focus on high-level system logic, workflow optimization, and stakeholder requirements.

### Where AI Was Wrong for My Case
The AI model demonstrated notable limitations in multi-source context reconciliation and case-specific constraint enforcement. Specifically:
1. **Missed Audio Correction:** The AI initially hallucinated a 1-week escalation rule based on the interview transcript (`01`), completely failing to recognize that the audio voice note (`02`) explicitly corrected this duration to 3 days.
2. **Ignored Staff Chat Context:** When asked to generate an initial database schema, the AI created a generic medical records ERD that omitted shelf-level misfile tracking, ignoring Mbak Rini's specific request in `04_Staff_Chat.png` to identify misfile shelf hotspots (e.g., Shelf 54).
3. **Over-Engineering Doctor Workflow:** The AI initially suggested adding status confirmation dropdowns for doctors, failing to uphold dr. Arif's strict constraint that doctors must type zero extra fields and experience zero operational delay.

### What I Can Now Do Without AI
Through this design experience, I have developed the critical domain competence to independently evaluate, model, and design health information systems. I can now:
* Conduct multi-source stakeholder requirement triangulation to detect and resolve contradictions between client statements, voice notes, and official hospital Standard Operating Procedures (SPOs).
* Build balanced, end-to-end system analysis models (Flowmaps, Context DFDs, Level 1 DFDs, and 5-entity ERDs) that perfectly match physical hospital archive workflows.
* Author comprehensive Product Requirements Documents (PRDs) with realistic, phased 3-round implementation plans that balance technical feasibility with clinical operational constraints.
* Defend every architectural entity, data flow, and functional requirement in an oral system design review without relying on automated AI summaries.
