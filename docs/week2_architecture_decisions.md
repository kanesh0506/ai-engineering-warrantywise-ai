# Week 2: Architecture Decisions and Traceability

## 1. Architecture Overview

WarrantyWise AI uses a simple step-by-step architecture to extract information from receipt images and help users track warranty dates.

The system consists of six main components:

1. **User** – Uploads receipts and reviews the results.
2. **Receipt Upload** – Accepts receipt images and checks file validity.
3. **AI Information Extraction** – Extracts product name, purchase date, price, and merchant name.
4. **Data Validation** – Organises the extracted information into JSON and identifies missing or unclear fields.
5. **Warranty Calculation** – Calculates the warranty expiration date when sufficient information is available.
6. **Results and User Review** – Displays extracted information and warnings for the user to check.

This architecture is designed to keep the system simple enough to develop and test within the available seven weeks.

## 2. Architecture Decision Records

### ADR 1: Use AI to Extract Receipt Information

**Problem:** Manually entering receipt information takes time, while receipt images may have different layouts.

**Options considered:**
- Option A: Ask users to enter all receipt information manually.
- Option B: Use OCR or an AI vision model to extract information from receipt images.

**Decision:** Choose Option B.

**Reason:** AI-based extraction reduces the amount of information users need to enter manually. Users can still review and correct the extracted results.

**Trade-off:** Extraction may be inaccurate when receipts are blurry, damaged, or difficult to read. The system must allow users to review the results.

### ADR 2: Validate Information Before Calculating Warranty Dates

**Problem:** AI may extract incomplete information or produce incorrect results. Calculating a warranty expiration date using unsupported information could mislead users.

**Options considered:**
- Option A: Display extracted information and calculate dates immediately.
- Option B: Validate the information and check for missing or uncertain fields before calculating dates.

**Decision:** Choose Option B.

**Reason:** Validation helps identify missing information and reduces the risk of showing unsupported warranty dates.

**Trade-off:** The system may not calculate an expiration date for some receipts. Users may need to check their warranty information manually.

### ADR 3: Use a Simple Sequential Architecture

**Problem:** A complex architecture would require more development time and make testing more difficult.

**Options considered:**
- Option A: Build a simple sequence of connected components.
- Option B: Build a more complex architecture with multiple independent services and integrations.

**Decision:** Choose Option A.

**Reason:** A sequential architecture is easier to develop, understand, and test within seven weeks. Each component has a clear responsibility.

**Trade-off:** The architecture may be less flexible if the system grows in the future. However, the simpler design is more suitable for the current project scope.

## 3. Traceability Matrix

The following table links the project objectives and requirements to the evaluation criteria, architecture components, and evidence that will be collected during testing.

| Objective | Requirement ID | Evaluation Criterion | Architecture Component | Evidence to Collect |
|---|---|---|---|---|
| O1: Extract receipt information | FR2 / NFR1 | Receipt information accuracy | AI Information Extraction | Compare extracted fields with manually checked information from 30 receipts. |
| O2: Produce structured information | FR3 / NFR4 | Valid JSON output | Data Validation | Record JSON schema validation results from 30 receipts. |
| O3: Handle uncertain information safely | FR4 / RAI1 | Handling missing or unclear information | Data Validation and Results and User Review | Test 10 receipts with missing or unclear information and record whether the system identifies the issues correctly. |
| O3: Support warranty tracking | FR5 | Correct warranty calculation | Warranty Calculation | Test cases with supported warranty durations and cases where the duration is unavailable. |

The evidence listed above will be collected during implementation and testing. These are planned tests, not completed results.

## 4. Reflection

**Which architecture decision was most important, and which requirement influenced it?**

ADR 2 was the most important decision because incorrect warranty information could mislead users. The decision was influenced by FR4 and RAI1, which require the system to identify missing or uncertain information. By validating the extracted data before calculating warranty dates, the system can avoid presenting unsupported information as confirmed facts.
