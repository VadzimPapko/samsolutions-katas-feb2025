# Architecture Decision Record (ADR): Use cases for Certificable, Inc Platform

## **Context**
The platform aims to streamline candidate testing, result assessment, and administrative workflows. Key actors include **Candidates**, **Administrators**, **HR**, **Experts** and  **AI Engenieer**.

Core use cases:
1. Candidates: take aptitude test; solve Case Study; submit solution; view Results; complaint process
2. Administrators: manage Candidate/Expert profiles; handle Complaints.
3. HRs: get certification results
4. Experts: manual grading
5. AI-Engineers: configure Workflows; add/edit Tests; fine-Tune Models.


## **Use Cases**

### **1. Candidate Interactions**
- **Aptitude test**
    - The candidate initiates and completes aptitude test.
- **Case Study**
    - The candidate initiates and completes case study.
- **Assess Submission**
    - The candidate submits their test responses for evaluation.
- **Results and Complaints**
    - The candidate views assessment results and submits complaints if discrepancies arise.

### **2. Administrator Interactions**
- **Administer Candidates and Experts Profiles**
    - The administrator manages user accounts and permissions for candidates and experts.
- **Results and Complaints**
    - Administrator addresses complaints submitted by candidates and ensures resolution.

### **3. HR Interactions**
- **Results and Complaints**
    - HR addresses complaints submitted by candidates and ensures resolution.

### **4. Experts**
- **Grading process**
    - Manual assess results based on AI-report from the system.

### **5. Administrator Interactions**
- **Add/Edit Tests and Case Studies**
    - The administrator creates or modifies tests and case study materials.
- **Configure System Workflows**
    - The administrator defines rules for test delivery, grading, and result distribution.
- **Fine Tune Models**
    - The administrator adjusts AI/ML models used for automated grading or analysis.


---

## **System Boundaries**
- The system encompasses test delivery, automated assessment, profile management, and certification workflows.
- External systems (e.g., Certifiable, Inc’s certification API) integrate via secure interfaces.

---

## **Key Interactions**
1. A **Candidate** completes tests and submits responses.
2. The system auto-grades submissions using AI models.
3. **Experts** evaluates the results and prepares a feedbak
4. The **AI engineer** ensures tests and workflows align with organizational needs.
5. **HR** get information according candidates result.
6. **Administrator** validates results and issues certifications.

---

This use case diagram ensures clarity in roles, responsibilities, and system functionalities, supporting scalable and secure assessment processes.  
