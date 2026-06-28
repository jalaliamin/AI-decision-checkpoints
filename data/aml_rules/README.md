# AML Rule Documents

This folder contains the anti-money laundering (AML) regulation documents used by the RAG-based fraud-screening agent in Module 5.

These documents are embedded into Qdrant as the knowledge base the agent retrieves from when screening cases for potential fraud.

---

## How these are used

In Module 5, students configure a RAG pipeline in n8n that:

1. Embeds the documents in this folder into a Qdrant vector store (done once during setup).
2. At runtime, retrieves the most relevant AML rule chunks given a case description.
3. Passes the retrieved context and case details to a local LLM (Ollama) to produce a structured fraud-screening decision.

The data science team's reported characteristics apply to this agent: very low false negatives, some false positives due to class imbalance. Students are expected to reason about when the agent's output can be trusted autonomously and when a human reviewer must remain in the loop.

---

## Files

| File | Rule | Risk level |
|---|---|---|
| `AML_RULE_001_MONEY_MULE_PASS_THROUGH.txt` | Money mule / pass-through account behavior | Critical |
| `AML_RULE_002_THIRD_PARTY_FUNDS_UNKNOWN_SOF.txt` | Third-party funds / unknown or undocumented source of funds | High |
| `AML_RULE_003_RAPID_MOVEMENT_CASH_OUT.txt` | Rapid movement / same-day forwarding / cash-out pattern | High |
| `AML_RULE_004_AVOID_SCRUTINY_AVOID_BANKS.txt` | Avoiding scrutiny / avoiding banks / avoiding attention | Critical |
| `AML_RULE_005_PROFILE_ACTIVITY_MISMATCH.txt` | Customer profile vs expected activity mismatch | Medium to High |
| `AML_RULE_006_MULTI_COUNTRY_VAGUE_CORRIDORS.txt` | Multiple countries / high-risk corridors with vague purpose | Medium to High |

Each file follows the same structure: rule ID, rule name, risk level, definition, trigger conditions (text indicators), AML rationale, and action/outcome.

---

## Note for instructors

The rules are intentionally written as text-based policy documents rather than structured data, which makes them realistic inputs for a RAG pipeline. Students must configure chunking, embedding, and retrieval appropriately for this format.

The class-imbalance characteristic reported by the data science team (high recall, some false positives) is a design choice: it ensures the fraud-screening agent flags the 20% of cases requiring human review rather than silently clearing them. Students should reason about this trade-off explicitly in their CP5 governance dossier.

---

*Part of the Banking Teaching Case. See the root README for the full course structure.*
