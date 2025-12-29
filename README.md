# ICD Version Mapping Tool  
### Unified Migration of ICD-9 and ICD-10 Datasets to ICD-11

---

## 📌 Overview

The **ICD Version Mapping Tool** is a research-oriented clinical informatics system designed to **translate diagnosis codes from legacy ICD versions (ICD-9, ICD-10, ICD-10-CM)** into **ICD-11 (MMS)**.

The primary goal is to **maximize dataset usability** by enabling historical and multi-source datasets to be harmonized under a single, modern ICD standard.

> ⚠️ This tool focuses on **ICD-to-ICD mapping**, not automated clinical coding from free text.

---

## ❓ Why This Tool Is Needed

Healthcare datasets are fragmented across ICD versions:

- Older datasets (e.g., MIMIC-III, claims data, registries) use **ICD-9 or ICD-10**
- Modern research, reporting, and analytics increasingly require **ICD-11**

Existing solutions (GEMs, WHO crosswalk tables) are:
- static lookups,
- incomplete,
- non-reciprocal,
- and lack confidence scoring or safety checks.

There is currently **no open, intelligent, explainable system** that:
- maps ICD-9 and ICD-10 datasets into ICD-11,
- preserves clinical intent,
- quantifies uncertainty,
- and supports large-scale batch processing.

This project addresses that gap.

---

## 🎯 Purpose and Use Cases

### Primary Purpose
> Enable reuse of legacy ICD-9 and ICD-10 datasets by translating them into ICD-11.

### Key Use Cases
- 📊 Research data harmonization  
- 🧬 Longitudinal and population studies  
- 🤖 Machine learning and benchmarking experiments  
- 🧾 Secondary analysis of administrative or registry data  

### What This Tool Is **Not**
- ❌ Not an automated clinical coder  
- ❌ Not a replacement for professional coders  
- ❌ Not a regulatory or billing system  

This is a **decision-support and data harmonization tool**.

---

## 🧠 Why Simple Crosswalks Are Insufficient

ICD revisions are **not backward-compatible taxonomies**.

Key challenges:
- **Non-reciprocal mappings** (one-to-many, many-to-many)
- **Granularity mismatch** between versions
- **Conceptual redesign** in ICD-11 (Foundation model, MMS, post-coordination)
- **Incomplete coverage** of ICD-10-CM in WHO tables

➡️ As a result, mapping is a **reasoning and validation problem**, not a lookup problem.

---

## 🧩 Design Philosophy

The tool is built around five core principles:

1. **Accuracy over automation**  
2. **Explainability by design**  
3. **Clinical safety first**  
4. **Modular architecture**  
5. **Clear versioned scope**

Ambiguous mappings are **flagged**, not forced.

---

## 📦 Scope and Versioning

### ✅ Version 1 (Current Scope)

**Unidirectional mapping only:**
- ICD-9 / ICD-9-CM → ICD-11  
- ICD-10 / ICD-10-CM → ICD-11  

Target:
- ICD-11 **MMS codes**
- No automatic post-coordination synthesis

---

### 🔁 Version 2 (Planned)

- Bidirectional mapping:
  - ICD-11 → ICD-10
  - ICD-11 → ICD-9
- Strong safeguards against false specificity
- Reverse-mapping uncertainty modeling

---

### 🔮 Future Work (Out of Scope)

- SNOMED CT → ICD-O-3 mapping (oncology)
- ICD-11 post-coordination generation
- Registry-grade oncology coding
- Regulatory or production deployment

---

## 🏗️ High-Level Architecture

### Conceptual Pipeline

1. Batch input ingestion  
2. Candidate generation (official mappings first)  
3. Sequential bridging (ICD-9 → ICD-10 → ICD-11)  
4. Candidate ranking:
   - lexical similarity
   - semantic similarity
   - hierarchical consistency  
5. Uncertainty quantification  
6. Decision gate (auto-select vs human review)  
7. Explainable output  

---

### Why Sequential Mapping?

Direct ICD-9 → ICD-11 mappings are sparse or unavailable.

Using **ICD-10 as an intermediary**:
- increases coverage,
- reduces semantic jumps,
- aligns with WHO transition logic.

---

## 📤 Output Format

For each source code, the tool returns:

- Source ICD code and version
- Top-K ICD-11 candidate codes
- Confidence score (0–10)
- Uncertainty rate (entropy-based)
- Mapping path trace
- Flags (e.g., `ROLLED_UP`, `ONE_TO_MANY`, `REVIEW_REQUIRED`)

This ensures **transparency, auditability, and safe downstream use**.

---

## 📊 Evaluation Framework

### Metrics Used
- Coverage rate  
- Precision / Recall / F1  
- Hierarchical match score  
- Rank-weighted precision  
- Uncertainty rate (entropy)  
- Standardization loss (roll-up impact)  

### Human-in-the-Loop
Some mappings are inherently ambiguous.  
Human review is **mandatory** beyond defined uncertainty thresholds.

This is a **feature**, not a limitation.

---

## ⚠️ Risk Management and Safety

### Known Risks
- Loss of specificity during roll-up
- Meaning drift in many-to-many mappings
- False certainty in ambiguous cases

### Mitigations
- Entropy-based uncertainty detection
- Hierarchical consistency scoring
- Conservative confidence thresholds
- Explicit review flags

---

## 🧠 Gap Statement

> While official crosswalks and equivalence tables exist for ICD transitions, there is currently **no intelligent, explainable, clinically aware system** that performs automated ICD-to-ICD mapping across versions—particularly from ICD-9 and ICD-10 into ICD-11—while quantifying uncertainty and preserving clinical intent.

This tool is designed to fill that gap.

---

## 🚀 Project Status

- ✅ Conceptual design completed  
- ✅ Literature-aligned architecture defined  
- ⏳ Implementation (V1 batch mapping) in progress  

---

## 📌 Next Steps

- Implement ICD-10 → ICD-11 batch mapping
- Add ICD-9 → ICD-11 sequential mapping
- Integrate ranking and uncertainty modules
- Publish evaluation results

---

## 👤 Author

**Abdelrhman Akram Youssef**  
Biomedical Informatics  
Nile University  

---

## 📄 License

This project is intended for **research and academic use**.  
Licensing details will be finalized upon public release.

