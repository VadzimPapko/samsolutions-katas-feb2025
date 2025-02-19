# Architecture Decision Record (ADR): Certification Process (Test 2: Architecture Solution)

## **Title**
Solution for Certification Process (Test 2: Architecture Solution)

## **Context**

Candidates must pass Test 1 to qualify for Test 2.  
The system randomly assigns one of five pre-defined case studies to the candidate.

Candidates design an architectural solution for the assigned case study.  
The solution must address technical requirements, scalability, maintainability, and align with business goals.  
Candidates upload their solution via the `Architecture Submission Service`.  
The submission is stored in the `Submission Ungraded Database` for expert review.

Employed expert software architects retrieve submissions from the database. Each submission takes ~8 hours to grade, with detailed feedback provided.  
Results are stored, and candidates receive an email with their grade, feedback, and certification status within 1 week of submission.

**Certifiable, Inc.** faces scalability challenges due to anticipated 5-10X growth in certification requests.

---

## Main Changes

### Decision
Integrate an **AI Grading Service** leveraging Large Language Models (LLMs) and Retrieval-Augmented Generation (RAG) to:
- Automate preliminary grading of architecture submissions.
- Augment human graders by providing suggestions and identifying patterns.
- Generate new test cases dynamically using LLMs to prevent case study leakage.
- Validate candidate complaints via AI-driven prompt filtering and response generation.

### Key Components
- **LLM Core**: For grading logic, feedback generation, and test case creation.
- **Vector Database**: Stores embeddings of historical graded solutions and approved architectural patterns for RAG.
- **Embedding Pipeline**: Converts candidate submissions into embeddings for similarity analysis.
- **Prompt Validation Layer**: Ensures candidate/system prompts adhere to guidelines.
- **Response Filter**: Sanitizes AI-generated feedback to eliminate inaccuracies or biases.
- **AI Grading Orchestrator**: Coordinates AI-expert collaboration (e.g., preparing full reports based on scoring; flagging edge cases for human review).
- **Multi-Model Usage for Grading**: Improves accuracy by leveraging domain-specific expertise.
- **Automated Test Case Mutation**: Extends the LLM-driven test case generator to create "mutated" case studies.

---

## Alternatives

### Hire Additional Graders
- **Pros**: Maintains human judgment.
- **Cons**: Costly, slow to scale, and incapable of scaling to worldwide needs.

### Rule-Based Automation
- **Pros**: Predictable outcomes.
- **Cons**: Inflexible for complex architectural evaluations; requires constant rule updates.

### Hybrid AI-Human Workflow (Chosen Solution)
- Balances automation with expert oversight, ensuring accuracy while scaling efficiently.

---

## Consequences

### Positive
- **Scalability**: Reduces grading time, enabling handling of 5-10X volume.
- **Cost Efficiency**: Lowers reliance on manual grading experts.
- **Dynamic Test Cases**: LLM-generated case studies mitigate leakage risks.
- **Consistency**: Embedding-based similarity checks reduce grading subjectivity.
- **Human-in-the-Loop**: Experts review AI-generated grades and feedback before finalizing.
- **Candidate Trust**: Clear transparency measures accompany AI usage in grading.

### Negative
- **Model Accuracy Risks**: LLM hallucinations or biases require robust validation.
- **Integration Complexity**: Adds dependencies on AI infrastructure (vector DB, LLM APIs); introduces new AI-engineer role.
- **Monitoring Overhead**: Requires observability pipelines to audit AI decisions.
- **Guardrails**: Implement strict response filtering and fallback to human graders for low-confidence AI results.

---

## Future Improvements

### Dynamic Active Learning Integration
**Improvement**  
Integrate a learning pipeline to iteratively improve the AI grading model. The AI service flags submissions where grading confidence is low, prompting human experts to review them.

**Benefits**
- Continuously enhances model accuracy by learning from edge cases.
- Reduces long-term reliance on manual grading for ambiguous submissions.
- Aligns with the existing human-in-the-loop workflow.

**Implementation**
- Add a `Confidence Score Threshold` to the `AI Grading Orchestrator`.
- Use the `Vector Database` to store newly labeled data (human-reviewed submissions) for model retraining.
- Schedule periodic model retraining cycles using updated datasets.

---

### Real-Time Candidate Feedback Portal
**Improvement**  
Build a self-service portal where candidates can track submission status in real-time and view preliminary AI-generated feedback (before expert review).

**Benefits**
- Enhances transparency and candidate experience.
- Reduces administrative overhead in handling complaints.

---

### AI-Driven Education Portal or AI Tutor (Virtual Assistant)
**Improvement**  
Introduce an AI-Driven Education Portal to complement Certifiable, Inc.’s certification process. This portal will provide candidates with personalized learning resources, practice tools, and real-time feedback to better prepare for Test 1 (Aptitude) and Test 2 (Architecture Solution).

**Benefits**
- Targeted preparation reduces candidate knowledge gaps.
- Engaging tools (AI Tutor, community hub) improve user satisfaction.
- Portal analytics identify common weaknesses to refine certification exams.

**Implementation**
1. Build core features: `Practice Exam Service`, `Resource Library`, and `Progress Dashboard`.
2. Integrate with the `AI Grading Service` for practice test feedback.
3. Implement personalized learning paths using `Vector Database` embeddings.
4. Launch the moderated forum and observability dashboards for portal usage.  
