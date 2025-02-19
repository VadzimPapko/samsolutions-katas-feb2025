# AI Integration

The AI Grading Service is designed to automate the grading process for the Case Assessment. This service leverages machine learning algorithms to evaluate and score submissions efficiently.

### Architecture Overview

The architecture diagram below illustrates the components and their interactions within the AI Grading Service.

![AI Grading Service Architecture](/architecture-solution/diagrams/Kata2025-Test2-ai-grading-service.png)

For more details, refer to the [ADR documentation](architecture-solution/adr/02_adr_test2_ai_grading_service_details.md).

### Components

#### 1. Task Queue Processing
The "Task Processing Service" is a core component responsible for receiving, validating, analyzing, and executing tasks. It integrates AI, specialized agents, and workflow management to ensure efficient and secure task handling, and controls the infrastructure load.

#### 2. Prompt Validation and Structured Output
This process uses "Nemo Guardrails" to ensure that candidate results meet specific criteria before they are processed.

- **Workflow**:
    - Checks for malformed inputs or malicious content.
    - Rejects invalid prompts or flags them for manual review.
- **Advantages**:
    - Ensures data integrity and security.
    - Reduces downstream processing errors.
- **Drawbacks**:
    - Dependency on Nemo Guardrails updates for new validation criteria.

#### 3. Submission Transforming
After validation, the prompts are processed to transform raw task inputs into standardized formats ("structured output").

- **Workflow**:
    - Applies filters, formatting, or enrichment to outputs.
    - Prepares data for LLM analysis, divided by architecture sections.
- **Advantages**:
    - Simplifies data consumption for other roles.
- **Drawbacks**:
    - Lack of transparency in processing logic complicates debugging.

#### 4. Router
The **router** acts as a central hub that directs the processed data to different specialized agents based on the requirements.

#### 5. Agents
- **Key Agents**:
    1. **Agent for Functional Requirement**: Handles tasks related to functional requirements (ensures tasks align with business logic).
    2. **Agent for Non-Functional Requirement**: Manages performance, security, and scalability aspects.
    3. **Agent for Processing General Solution**: Processes general solutions (analyze architecture style, suggested technologies).
    4. **Agent for Processing Diagrams**: Interprets visual diagrams (e.g., flowcharts, architecture diagrams).
    5. **Agent for Cost Calculation**: Manages cost calculations for infrastructure, licenses, etc.

- **Advantages**:
    - Specialization improves task-handling efficiency.
    - Clear separation of concerns (e.g., functional vs. non-functional).
- **Drawbacks**:
    - Diagram agent requires frequent updates to stay aligned with system changes.

Each agent receives a special system prompt tailored for a specific "case study" and processes it accordingly.

#### 6. System Prompts & Test Result Analyzer Based on LLM
Each agent has its own system prompt for each case study, which ensures that the outputs from the agents are accurate and meet the desired standards.

#### 7. Scoring System & AI Grading Orchestrator
The analyzed results are then scored separately by each agent.

#### 8. Additional Services
The workflow management is based on LangGraph, which helps in orchestrating the entire process.
An observability module based on LangSmith monitors the system to ensure smooth operation and troubleshoot any issues.
### Summary
This architecture is designed to handle a variety of tasks efficiently by leveraging specialized agents, LLMs, and a robust workflow management system. It ensures that each task is processed accurately and evaluated thoroughly, with mechanisms in place for monitoring and manual intervention if necessary.



