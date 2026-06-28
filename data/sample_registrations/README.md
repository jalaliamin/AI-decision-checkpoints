# Sample Customer Registration Documents

This folder contains sample customer registration PDF forms used in the email-intake agent lab.

In Module 1 (Lab 1) and Module 5, students build and extend an AI agent that reads incoming customer registration emails and extracts structured data from attached PDF forms using a local LLM (Ollama). These 14 sample documents serve as realistic test inputs.

---

## How these are used

**Module 1 - Lab 1:** Students send a sample registration email with one of these PDFs attached to a local mail server (smtp4dev). Their n8n workflow triggers on arrival, extracts the PDF, and passes it to an Ollama-served LLM for structured data extraction. The output is a JSON record representing the registered customer.

**Module 5:** The same agent is integrated into the full end-to-end onboarding workflow. Students use these documents to test the pipeline including the failure fallback path to a manual clerk node.

---

## Files

| File | Description |
|---|---|
| `01.pdf` - `14.pdf` | Sample customer registration forms (14 cases) |

Each PDF represents one customer registration request. The agent is expected to extract the relevant customer fields and return a structured JSON record.

---


*Part of the Banking Teaching Case. See the root README for the full course structure.*
