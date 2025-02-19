# Architecture Decision Record (ADR): AI Grading Service

## **Title**
System Architecture Overview for AI Grading Service

## **Context**
The architecture depicted in the diagram is a complex system designed to process tasks, validate prompts, and analyze
results using various agents and large language models (LLMs). Below is a detailed breakdown of its components and flow:

# Components

## 1. Task Queue Processing
The "Task Processing Service" is a core component of the IT architecture, responsible for receiving, validating, analyzing, and executing tasks. It integrates AI, specialized agents, and workflow management to ensure efficient and secure task handling, and  controls the infrastructure load.

## 2. Prompt Validation and Structured Output
This process uses "Nemo Guardrails" to ensure that candidate result meet specific criteria before they are processed.
NeMo Guardrails is an open-source toolkit for easily adding programmable guardrails to LLM-based conversational applications. Guardrails (or "rails" for short) are specific ways of controlling the output of a large language model, such as not talking about politics, responding in a particular way to specific user requests, following a predefined dialog path, using a particular language style, extracting structured data, and more.

- **Workflow**:
    - Checks for malformed inputs or malicious content.
    - Rejects invalid prompts or flags them for manual review.
- **Advantages**:
    - Ensures data integrity and security.
    - Reduces downstream processing errors.
- **Drawbacks**:
    - Dependency on Nemo Guardrails updates for new validation criteria.


## 3. Submission transforming
After validation the prompts are processed to transform raw task inputs into standardized formats ("structured output").

- **Workflow**:
    - Applies filters, formatting, or enrichment to outputs.
    - Prepares data for LLM analysis, divide by architecture sections.
- **Advantages**:
    - Simplifies data consumption for other roles.
- **Drawbacks**:
    - Lack of transparency in processing logic complicates debugging.

## 3. Router

The **router** acts as a central hub that directs the processed data to different specialized agents based on the requirements.

## 4. Agents

- **Key Agents**:

1. **Agent for Functional Requirement**: Handles tasks related to functional requirements (ensures tasks align with business logic).
2. **Agent for Non-Functional Requirement**: Manages performance, security, and scalability aspects.
3. **Agent for Processing General Solution**: Processes general solutions (analyze architecture style, suggested technologies).
4. **Agent for Processing Diagrams**: Interprets visual diagrams (e.g., flowcharts, architecture diagrams).
5. **Agent for Cost Calculation**: Manages cost calculations for infrastructure, licences, etc .

- **Advantages**:
    - Specialization improves task-handling efficiency.
    - Clear separation of concerns (e.g., functional vs. non-functional).
- **Drawbacks**:
    - Diagram agent requires frequent updates to stay aligned with system changes.

Each agent receives a special system prompt tailored for a specific "case study" and processes it accordingly.

## 5. System Prompts & Test Result Analyzer Based on LLM

Each agent has its own system prompt for each case study, which in turn ensures that the outputs from the agents are accurate and meet the desired standards.

example, input query:

```javascript
{
"question": "assess the architecture solution according scroing model",
"candidate_answer": "structured outputs from step 2",
"evaluation_criteria": {
  "technical requirements": 0.3,
  "scalability": 0.2,
  "documentation level": 0.1,
  "observabiity": 0.1,
  "perfomance": 0.1,
  "security risks": 0.1,
  "observabiity": 0.1          
  }
}
```


## 6. Scoring System & AI Grading Orchestrator

The analyzed results are then scored separately by each agents.

example, score result output for non-functional requirement
```javascript

{
    "score": 0.79,
    "criteria_scores": {
        "technical requirements": 0.9,
        "scalability": 0.9,
        "documentation level": 0.8,
        "observabiity": 0.8,
        "perfomance": 0.6,
        "security risks": 0.6,
        "observabiity": 0.9
    },
    "feedback": "Your answer is well structured, but you could add more details about the technologies you chose, such as...."
}
```

The **AI Grading Orchestrator** is a service that automates, and sunmmarizes the evaluation of tasks, outputs, or solutions within the IT architecture.

# 7. Additional Services

- The **workflow management** is based on LangGraph, which helps in orchestrating the entire process.
- An **observability module** based on LangSmith monitors the system to ensure smooth operation and troubleshoot any
  issues.


# Summary

This architecture is designed to handle a variety of tasks efficiently by leveraging specialized agents, LLMs, and a
robust workflow management system. It ensures that each task is processed accurately and evaluated thoroughly, with
mechanisms in place for monitoring and manual intervention if necessary.
