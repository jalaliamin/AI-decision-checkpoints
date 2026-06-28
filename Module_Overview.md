# Module Overview: AI-Decision Checkpoints Banking Case

Six modules aligned with the BPM lifecycle. Each module's output is the next module's input (evolving-artifact structure).

---

## Module 1: Introduction to BPM and AI Foundations

**Lifecycle phase:** Process Identification
**AI-Decision Checkpoint:** CP1 - Scope AI opportunities
**Primary tools:** n8n, Ollama
**Assessment:** Assignment 1 (Pass / Fail)

### Lectures

1. **History and evolution of BPM** - From Adam Smith's division of labor through scientific management, assembly lines, quality and lean methods, workflow systems, BPMS and the internet era, RPA and process mining, to AI agents and intelligent automation. Each era introduced a solution to a problem the previous era could not handle.

2. **Introduction to business process models** - What a business process is (activities performed in coordination in an organizational and technical environment to realize a business goal). The difference between normative models (how the process should work), descriptive models (how it actually works) and executable models (models with formal semantics which are understandable by software). Why informal descriptions fail at scale and why precision matters.

3. **The BPM lifecycle** - The six-phase cycle: process identification, discovery, analysis, redesign, implementation, and monitoring and controlling. Why the lifecycle is a loop rather than a line. The role of executable models in making analysis and redesign rigorous rather than guesswork.

4. **Porter's Value Chain** - How individual processes sit inside a larger organizational value creation system. Primary activities and support activities for a retail bank. Why process improvement decisions should be anchored in the strategic picture before zooming into a single process.

### Lab 1: AI-Enhanced Workflows in n8n

Students build a working AI email-intake agent from scratch inside n8n. The agent reads incoming customer registration emails, extracts structured data from PDF attachments using a local LLM (Ollama), and outputs a clean JSON record ready for a banking system. Eight tasks build the agent step by step: PDF extraction with an online LLM, repeating extraction with a local Ollama model, verifying Docker containers, setting up the mail server (smtp4dev), exploring the n8n editor, building an email-trigger workflow, adding a PDF extraction node, and adding an AI agent node with structured output parsing.

After completing the lab, students are asked: if the bank deployed this agent tomorrow, would the onboarding process actually improve? This question - the gap between "the technology works" and "we do not yet know if it adds value" - is the central tension the rest of the course is designed to resolve.

### Lecture: AI-Augmented BPM and the Checkpoint Framework

Introduces the bottleneck shift trap: automating a step that is not the bottleneck does not improve end-to-end performance and can make things worse by feeding work into a constrained downstream resource faster. Presents the two complementary deficits in current industry practice: the classically trained BPM analyst who cannot reason about AI adoption, and the AI engineer who cannot assess process-level impact. Introduces the concept of an AI-Augmented Business Process Management System (ABPMS) and the AI-decision checkpoint framework as a bridge.

### Assignment 1: Process Architecture and AI Opportunity Register (CP1)

**Deliverable 1 - Porter's Value Chain for Nordic Secure Bank.** Students draw a value chain with primary and support activities adapted for a retail bank, anchor the customer onboarding process explicitly as a primary activity, trace case-specific roles and systems into the support activities, and add a short explanation of why improving onboarding matters for the bank's overall value creation.

**Deliverable 2 - CP1: AI Opportunity Register.** Students identify at least two sub-processes in the onboarding case as AI candidates (focusing on email-based registration and fraud assessment). For each candidate they assess impact along the devil's quadrangle (time, cost, quality, flexibility), note key risks in the banking context (GDPR, false positives in fraud screening, regulatory constraints), and state which candidate they would prioritise and why. The register is explicitly provisional and will be revisited at each subsequent checkpoint as evidence accumulates.

Format: single PDF, one submission per group. 

---

## Module 2: Process Modeling and the Token Game

**Lifecycle phase:** Process Discovery
**AI-Decision Checkpoint:** CP2 - Position AI candidates in the as-is model
**Primary tools:** draw.io, pm4py (Jupyter notebook)
**Assessment:** Assignment 2 (Pass / Fail)

### Lectures

1. **Workflow pattern language** - Three layers: notation (activity as rounded rectangle, control-flow element as labeled circle, flow as directed arrow), syntax (rules for connecting symbols), and semantics (the token game). Eight fundamental patterns: sequence, parallel split, synchronization, exclusive choice, simple merge, multi-choice, structured synchronizing merge, and deferred choice. Each pattern is defined by how tokens are produced and consumed.

2. **Process model correctness** - Syntactic correctness and semantic correctness. The distinction matters because a syntactically valid model can still describe a process that deadlocks or duplicates work.

3. **Process complexity and presentation** - Loop patterns (structured loops and arbitrary cycles). Complexity metrics: NOA (number of activities), NOAC (activities plus split/join pairs, defined only for block-structured models), and NOAJS (activities plus all splits and joins individually). Presentation patterns for reducing complexity deliberately, including compacting and block structuring.

4. **Process trees** - A tree-based representation of block-structured process models. Operators (sequence, exclusive choice, parallel, loop) as internal nodes; activities as leaves. The PTML textual format. Connection to Module 6.

### Lab 2: Workflow Patterns in n8n

Students implement each of the eight workflow patterns directly in n8n and evaluate the platform's pattern support. The perspective is that of a chief IT officer assessing n8n for use in the bank's onboarding process. Students work through seven tasks, each implementing one or more patterns, then compile a pattern support summary table (native support, workaround required, or not expressible). This evaluation feeds directly into the CP2 deliverable.

### Lab 3: Process Trees in Python

Students write a PTML file by hand for a given process tree, load it with pm4py in a Jupyter notebook, and visualise the result. The lab gives hands-on familiarity with the PTML format and pm4py tooling that returns in Module 6.


### Assignment 2: Normative As-Is Model and CP2

**Deliverable 1 - Normative As-Is Model.** Students model the normal scenario of the banking onboarding process in draw.io using the workflow pattern language from this module (rounded rectangles, labeled control-flow circles). Every activity must use verb-object naming (e.g., "Check customer credit" not "Credit check") and be annotated with the role that performs it (Anna, Kim, Elin, Paul, Linda, Peter, Maria). Students verify correctness by tracing the token game through at least two execution paths. 

**Deliverable 2 - CP2: AI-Positioning Note.** For each CP1 candidate, students specify: (1) the segment of the as-is model it would replace, support, or augment; (2) the human roles and systems currently involved and how they would be affected; (3) the inputs, outputs, and control transfers at that segment; and (4) at least one structural obstacle (for the email-intake agent: failure handling; for the fraud-screening agent: when high recall but imperfect precision means a human must remain in the loop). The note ends with a paragraph revisiting the CP1 priority ranking in light of the model.

Format: single PDF, model diagram first then positioning note. One submission per group. 

---


## Module 3: Process Analysis, Baseline Simulation, and CP3 and CP4 (pass 1)

**Lifecycle phase:** Process Analysis + initial Redesign
**AI-Decision Checkpoints:** CP3 - Quantitative baseline; CP4 (first pass) - Simulate redesign options
**Primary tools:** WoPeD, ProM

### Lectures and content

1. **Petri nets and workflow nets** - Formal foundations: places, transitions, tokens, firing rules. Workflow nets as a restricted class of Petri nets with a single source place and single sink place. Soundness criteria: option to complete, proper completion, and no dead transitions. Why soundness matters before simulation: an unsound model produces meaningless KPIs.

2. **Simulation in WoPeD** - Translating the as-is model from M2 into a workflow net. Configuring simulation parameters: case arrival rates, processing-time distributions (based on Document A timings), resource pools and capacities, routing probabilities (10% credit rejection, 80% no-fraud, 90% external investigation result within one day). Running the simulation and reading throughput time, waiting time, and resource utilisation outputs.

3. **Process analysis and bottleneck identification** - Exporting simulated logs from WoPeD to ProM. Applying performance spectrum analysis to surface bottlenecks visually. The key finding most groups encounter: the bottleneck is not in registration (20 minutes per case, one clerk) but in another part of the process.

4. **Redesign patterns and simulation of variants** - Recognized redesign principles: task elimination, resequencing, parallelisation, and integration of responsibilities. Constructing to-be scenarios that include both classical control-flow changes and AI-embedding designs. All variants are simulated under the same parameter assumptions and compared against the CP3 baseline.

### Document B released at this module

Students receive the management redesign request (Document B) at the start of M3. It specifies the three registration channels (AI agent 60%, online form 20%, manual clerk 20%), the AI agent failure rate (20% fallback to clerk), the web-service automations, and the fraud-screening agent characteristics (high recall, some false positives, 80% of cases classified as no-fraud automatically, 20% routed to manual review).

### CP3 artifact

A baseline performance report documenting the executable workflow-net model, simulation assumptions, and key performance indicators. The report highlights structural bottlenecks and systematic delays. CP3 does not deploy AI; it establishes the quantitative baseline against which all CP4 redesign variants are compared.

### CP4 artifact (pass 1)

A preliminary comparative redesign and simulation dossier. For each variant (classical and AI-embedding), the dossier records simulated KPIs relative to the CP3 baseline and assigns a preliminary redesign decision with justification, including trade-offs such as bottleneck relocation or increased process complexity. This report is finalised in M4 once the BPMN-level redesign is complete.

> CP4 is intentionally split across M3 and M4. The workflow-net pass in M3 grounds design choices analytically before students invest in BPMN exception-handling notation in M4. Many groups initially expect the email-intake agent to halve end-to-end cycle time; the CP3 baseline typically shows the bottleneck lies in fraud investigation, prompting a revision of that expectation before M4 begins.

---


## Module 4: BPMN-Centric Process Redesign and CP4 (pass 2)

**Lifecycle phase:** Process Redesign
**AI-Decision Checkpoint:** CP4 (second pass) - Exception handling, governance, implementability
**Primary tools:** Signavio, Trisotech

### Lectures and content

1. **BPMN 2.0 notation and execution semantics** - Token-based execution rules for BPMN elements: tasks, gateways, events, and subprocess boundaries. The distinction between the modelling view and the executable view. Why BPMN is chosen for M4 rather than M3: it has dedicated constructs for exception handling, cancellation, and compensation that workflow nets lack.

2. **Exception handling and cancellation in BPMN** - Boundary events (error, timer, cancel), event-based gateways, and compensation handlers. 

3. **Human-in-the-loop and AI fallback design** - Explicit modelling of human review steps for AI-supported tasks: approval gates, escalation paths, confidence-threshold triggers, and fallback activities for AI failure or low-confidence output. The fraud-screening agent path requires a manual review step for the 20% of cases flagged as potential fraud; this must be modelled explicitly, not assumed.

4. **Evaluating BPMN tools** - Students critically assess Signavio and Trisotech for model verification (syntax checking, soundness analysis) and simulation fidelity. This extends the platform evaluation perspective introduced in M2 (n8n) to the modelling toolset.

### CP4 artifact (pass 2, final)

A consolidated BPMN to-be model encoding the chosen redesign variant from M3, enriched with: all exception and escalation paths, human-in-the-loop review steps for AI-supported tasks, and AI-specific fallback behaviour (schema validation failures, low-confidence outputs, agent failure paths). Together with the simulation evidence from M3, this constitutes the final CP4 outcome and the direct input to M5 implementation.

---

## Module 5: Workflow Implementation and CP5

**Lifecycle phase:** Process Implementation
**AI-Decision Checkpoint:** CP5 - Realisability and governance
**Primary tools:** n8n, Ollama, Qdrant

### Lectures and content

1. **AI augmentation configuration patterns** - A taxonomy of how AI components can be integrated into workflow platforms: human-only, rule-based, LLM-based, RAG-equipped, and multi-agent configurations. Each pattern has different data flow requirements, error-handling needs, and governance implications. Students use this taxonomy to plan their implementation before touching a platform.

2. **Mapping BPMN to n8n** - Translating the M4 BPMN to-be model into an executable n8n workflow. Where n8n's node types map cleanly onto BPMN constructs and where they do not. Compensating structures for unsupported patterns: additional validation nodes, schema-constrained prompt templates, explicit error-branch wiring, and manual trigger nodes for human approval steps.

3. **Implementing the email-intake agent** - Connecting the n8n email trigger to an Ollama-served local LLM. Prompt engineering for structured extraction from PDF attachments. Schema-constrained output parsing to prevent malformed JSON from propagating downstream. Configuring the 20% failure fallback path to a manual clerk node.

4. **Implementing the fraud-screening RAG agent** - Embedding AML rule documents into Qdrant as a vector store. Configuring the RAG retrieval step and LLM reasoning step within n8n. Setting a confidence threshold: cases where the agent returns "no fraud" with high confidence proceed automatically; the 20% flagged as potential fraud route to an explicit human-approval node. Logging all agent decisions for audit purposes.

5. **Governance and residual risk** - For each AI component: what logging is in place, which thresholds trigger human intervention, what escalation rules apply, and what residual technical or organisational risks remain after implementation. Students find that reasoning through governance at implementation time often converts abstract BPMN governance constructs into concrete workflow controls they had not fully specified in M4.

### CP5 artifact

An implementation feasibility and governance dossier per AI component, documenting: (i) the extent to which each component was realised as designed in M4, (ii) workarounds introduced (schema-constrained prompts, fallback paths, additional validation activities), (iii) governance mechanisms put in place (logging, confidence thresholds, escalation rules, human-in-the-loop points), and (iv) residual technical or organisational risks. Students who modelled a fraud-screening approval step in BPMN often add a concrete human-approval node in n8n once they encounter structured-output reliability limitations of the local LLM, converting a conceptual governance requirement into a tangible workflow control.

---

## Module 6: Process Mining and CP6

**Lifecycle phase:** Process Monitoring and Controlling
**AI-Decision Checkpoint:** CP6 - Mining-based evaluation
**Primary tools:** ProM, PM4Py, Celonis

### Lectures and content

1. **Event log fundamentals** - What an event log is: cases, events, activities, timestamps, resources, and lifecycle transitions (start/complete). The IEEE XES format. ETL considerations: extracting logs from operational systems, handling missing data, filtering noise. The assumption students must resist: that the log represents a single stable process. Object-Centric Event Log (OCEL) format. 

2. **Concept drift** - How process behaviour changes over time due to organisational restructuring, staffing changes, or technology introductions. Types of drift: sudden, gradual, recurring, and seasonal. Why segmenting a log before discovery produces more accurate models than mining the full log at once. The synthetic event log for this module contains at least one drift point that students are expected to detect and characterise.

3. **Process discovery algorithms** - Alpha Miner, Inductive Miner, and Heuristics Miner: what each optimises, where each fails, and how to choose. Model quality dimensions: fitness (the model can replay the log), precision (the model does not allow too much behaviour not in the log), simplicity (the model is as compact as possible), and generalisation (the model applies beyond the specific log). Students discover separate models for each drift-segmented period and evaluate them on all four dimensions.

4. **Conformance checking** - Comparing what the event log records against what the normative to-be model prescribes, using token-based replay or alignment-based techniques. 

5. **Performance analysis** - Quantifying realised performance indicators (throughput times, waiting times, resource utilisation) from the event log and comparing them to the CP3 simulation baseline and the CP4 simulated expectations. Answering the CP6 guiding question: do the AI-augmented subprocesses expected to deliver the value projected at redesign time based on how the process has changed over time?

### The synthetic event log

Students receive a multi-year synthetic event log of the onboarding process (see `event_log/`). The log is constructed to exhibit concept drift reflecting a change in how the process is executed over time (for example, the introduction of automated sub-processes). Activities correspond to the tasks in Document A and, in later log periods, to the automated variants from Document B. Resources are named after the case roles: Anna, Kim, Elin, Paul, Linda, Peter, and Maria.

Students must not assume the log represents a single stable process. The recommended sequence: visualise the full log (dotted chart), detect and characterise drift points, segment the log by period, mine models per segment, evaluate model quality, perform conformance checking against the M5 to-be model, and interpret findings against the CP3 baseline.

### CP6 artifact

A mining-based evaluation summary consolidating: discovered execution patterns per period, drift characterisation (location, type, and likely cause), conformance deviations relative to the M5 to-be model, and realised performance indicators relative to the CP3 baseline and CP4 projections. The summary concludes with a recommendation: do the AI-augmented subprocesses behave as intended, or should the process be redesigned and reconfigured? This recommendation feeds back into CP1, closing the evidence-based governance cycle.

---

## Checkpoint Summary

| CP | Phase | Guiding question | Key artifact |
|---|---|---|---|
| CP1 | Identification | Which sub-processes are plausible AI candidates? | AI opportunity register |
| CP2 | Discovery | Where do candidates attach in the as-is model? | Normative as-is model + AI-positioning note |
| CP3 | Analysis | What is the baseline performance? | Simulation report |
| CP4 | Redesign | Under which conditions does AI augmentation outperform the baseline? | Redesign and simulation dossier (2 passes) |
| CP5 | Implementation | Is the redesign technically realisable and governable? | Feasibility and governance dossier |
| CP6 | Monitoring | Will AI-augmented sub-processes behave as intended over time based on process execution history? | Mining-based evaluation summary |

---

*M1 and M2 content reflects actual course materials. M3-M6 descriptions will be updated when those materials are provided.*

*Part of the Banking Teaching Case. See the repository README for citation and instructor-material requests.*
