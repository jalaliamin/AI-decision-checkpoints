# Synthetic Event Log — Module 6

This folder contains the synthetic event log used in Module 6 (Process Monitoring and CP6).

---

## File

| File | Format | Description |
|---|---|---|
| `full_log.zip` | IEEE XES | Multi-year synthetic event log of the customer onboarding process (not sorted) |


---

## Log Description

The log simulates several years of customer onboarding executions at the fictitious bank. It is constructed to exhibit **concept drift** (gradual or sudden changes in process behaviour over time) reflecting organisational restructuring, changes in staffing, or the introduction of new technologies during the observation period.

### Key characteristics

- **Case notion:** One case = one customer onboarding request
- **Activities:** Correspond to the tasks described in Document A (and, in later periods, the automated variants from Document B)
- **Resources:** Named after the roles in the case (Anna, Kim, Elin, Paul, Linda, Peter, Maria)
- **Timestamps:** Synthetic but realistic, preserving the processing-time distributions described in Document A
- **Concept drift:** At least one drift point is present; students are expected to detect and characterise it

### Attributes per event

| Attribute | Description |
|---|---|
| `case:concept:name` | Unique case identifier |
| `concept:name` | Activity name |
| `time:timestamp` | Event timestamp |
| `org:resource` | Resource (role) performing the activity |
| `lifecycle:transition` | `start` or `complete` |

---

## How to Use (Module 6)

Students should **not** assume the log represents a single stable process. The recommended analysis sequence:

1. Load the log in ProM or PM4Py and visualise it (dotted chart or similar) to identify candidate drift points.
2. Segment the log into coherent time periods based on detected drifts.
3. Discover separate process models for each period using multiple algorithms (e.g., Alpha Miner, Inductive Miner, Heuristics Miner).
4. Evaluate discovered models on fitness, precision, simplicity, and generalisation.
5. Perform conformance checking against the normative to-be model from M5.
6. Interpret findings in light of the CP3 baseline and CP4 simulated expectations.

---

*Part of the Banking Teaching Case repository. See the root README for the full course structure.*
