# Architectural Solution for Explainable Agentic AI Control Layer

## Introduction
### Background
Modern enterprise decision systems increasingly rely on semantic knowledge graphs and multi-agent reasoning frameworks. These systems can analyze policies, budgets, and operational constraints, and make human-like decisions through coordinated agent behavior.
However, for real-world adoption, organizations require **transparency**, **auditability**, and **human oversight** over automated decisions.
### Thesis Goal
This project aims to design and prototype an **XAI-driven control layer** that exposes the internal reasoning of a semantic decision-making system.
The goal is to provide:
    - human-readable explanations,

    - conflict detection and resolution insights,

    - structured decision traces,

    - and an interface for supervising or overriding agent decisions.

This prototype integrates:

    1. a lightweight ontology/knowledge graph,

    2. a multi-agent reasoning system, and

    3. an explainability + control interface.

## Goal
In this Architectural Solution document, I assume a **_hypothetical scenario_** where the goal is to design an **explainable Agentic AI Control Layer** that allows users to understand and interact with autonomous agents making complex decisions. 
This scenario involves the following key objectives:
1. Design a domain ontology that captures the relevant concepts, relationships, and decision-making criteria for the agents.
2. Design a knowledge graph (KG) that represents the ontology and supports semantic reasoning.
3. Design a multi-agent system where agents can autonomously make decisions based on the KG and progressively upskill their expertise.
4. Design an explainability layer that exposes the reasoning processes of the agents, allowing users to inspect decision paths, conflicts, and explanations.
5. Design a web-based interface that enables users to interact with the agents, monitor their actions, and provide feedback or overrides.

## Employee Trip Budget Approval (the hypothetical scenario)
### Scenario Description
1. In this scenario, we have an enterprise system where employees can submit trip requests for business travel.  
2. Each trip request includes details such as employee ID, destination, duration, purpose, and estimated costs.
3. Managers are responsible for reviewing and approving these trip requests based on company policies, budget constraints, and individual employee entitlements.
4. The system should provide transparency into the decision-making process, allowing employees and managers to understand why certain requests were approved or denied (Explainability).
### Ontology Design
#### Why Ontology?
1. An ontology provides a structured representation of the key concepts and relationships in the trip approval domain
2. It enables semantic reasoning by defining classes, properties, and constraints that capture the decision-making criteria.
3. It facilitates interoperability and knowledge sharing among different agents and components in the system.
#### Ontology Components
1. Key concepts: Employee, TripRequest, Manager, ApprovalDecision, CompanyPolicy, Budget, Entitlement.
2. Relationships: Employee submits TripRequest; Manager reviews TripRequest; ApprovalDecision is based on CompanyPolicy, Budget, and Entitlement.
3. Entity Relationship Diagram (ERD):

![Trip Approval Ontology ERD](images/ontology.png)
   
### Knowledge Graph Implementation by relational Database
For the prototype, I model the ontology as a lightweight semantic schema stored in a relational structure.
In the full thesis, this can be replaced with a proper RDF/graph store (Neo4j / GraphDB)
1. Tables: Employees, TripRequests, Managers, ApprovalDecisions, CompanyPolicies, Budgets, Entitlements.
2. Relationships: Foreign keys to represent relationships between entities (e.g., TripRequests linked to Employees and Managers).
3. Semantic reasoning: Implement rules and constraints to evaluate trip requests based on policies, budgets, and entitlements.
4. Example of relational databases: MySQL, Oracle, and etc.

### Multi-Agent System
1. Agents: TripRequestAgent, ApprovalAgent, PolicyAgent, BudgetAgent, EntitlementAgent.
2. TripRequestAgent collects trip requests and forwards them to ApprovalAgent. 
3. ApprovalAgent coordinates with PolicyAgent, BudgetAgent, and EntitlementAgent to evaluate requests.
4. Each agent uses the knowledge graph database to access relevant data and make decisions.
5. Agents log their reasoning steps and decisions for explainability.
**Example Explanation Output:**
Trip denied because the estimated cost (4000 SEK) exceeds the employee entitlement (2500 SEK) and violates company policy rule P3.

This is the type of human-readable explanation that the control layer will display, showing the key factors behind the decision.

![Multi Agent System](images/multi_agent_system.png)

### Dig into a sample Agent (TripRequestAgent)
In this section, we will explore the architecture and functionality of the TripRequestAgent.


![Trip_Request_AI_Agent](images/Trip_Request_AI_Agent.png)
This diagram illustrates the internal components and workflow of the TripRequestAgent:
1. How AI Agent interacts with the Explainability Database to log decision traces.
2. How AI Agent communicate with LLM includes tools calling to enhance decision-making.
3. The logs and decision traces are stored in the Explainability Database for later retrieval and analysis.


### Explainability Layer
1. Capture decision paths: Each agent records the reasoning steps taken to arrive at a decision.
2. Conflict resolution: Highlight any conflicts between agents and how they were resolved.
3. Prioritized explanations: Generate human-readable explanations for each decision, focusing on the most relevant factors.
4. Progressive disclosure: Allow users to explore explanations at different levels of detail.

### Explainability Data Model
1. DecisionTrace: Records the sequence of reasoning steps taken by agents.
2. ConflictRecord: Captures conflicts between agents and their resolutions.
3. Session: Each request and its associated decision traces and explanations.

![Explainability_Data_Model](images/Explainability_Data_Model.png)

### Web-Based Interface
#### Sessions Management View
![Sessions_View](images/Sessions_Management_Dashboard_Overview.png)

### Workflow of Explainable Agentic AI Control Layer
![Workflow_of_Explainable_Agentic_AI_Control_Layer](images/Agents_WorkFlow.png)

### Agent Details View
![Agent_Details_View](images/Agent_Details.png)





