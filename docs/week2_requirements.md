# Requirements Specification — WarrantyWise AI

**Version:** 1.0

# Section 0 — Project Framing and Application Scope

## 0.1 Problem and Evidence

Consumers may have difficulty locating purchase information from receipts and remembering warranty expiration dates. Receipt images may contain unclear text, different layouts, or incomplete information, making manual recording and retrieval inconvenient.

For initial evidence, this project will examine sample purchase receipts to identify variations in layout, text clarity, and the availability of product and warranty information.

**References for technical background:**
- Google Cloud Vision OCR: https://cloud.google.com/vision/docs/ocr
- Pydantic: https://docs.pydantic.dev/
- JSON Schema: https://json-schema.org/learn/getting-started-step-by-step

These references explain relevant technical approaches. They do not, by themselves, establish how frequently consumers lose receipts or forget warranty dates. Such claims require separate supporting evidence.

## 0.2 Existing Approaches

### 1. Manual Receipt Management

Users can keep physical receipts or manually record purchase information. This approach requires users to organise and maintain the information themselves.

### 2. Optical Character Recognition (OCR)

OCR tools, such as Google Cloud Vision OCR, extract text from images. However, extracted text may still require interpretation to identify product names, purchase dates, prices, and other fields correctly.

### 3. Structured Data Validation

Tools such as Pydantic and JSON Schema can validate whether extracted information follows a predefined data structure. Structural validation alone does not guarantee that the information is factually correct.

## 0.3 Project / Engineering Gap

The engineering challenge is to combine receipt text extraction, information structuring, validation, and warranty date calculation in one workflow. The system must also identify missing or uncertain information and avoid presenting unsupported warranty estimates as confirmed manufacturer terms.

## 0.4 Project Objectives

- **O1:** To design a workflow for extracting relevant purchase information from receipt images.
- **O2:** To develop a system that structures and validates extracted information and calculates warranty expiration dates when sufficient information is available.
- **O3:** To evaluate the accuracy, processing performance, and responsible handling of uncertain information.

## 0.5 Application Scope

### Intended Users

Consumers who want to organise purchase receipts and keep track of product warranty information.

### Supported Tasks

- Upload receipt images.
- Extract available purchase information.
- Organise extracted information into structured JSON.
- Identify missing, unclear, or uncertain fields.
- Calculate warranty expiration dates when the required information is available.
- Display extracted information for users to review.

### Information / Knowledge Domain

Purchase receipts, product names, purchase dates, prices, merchant names, and available warranty information.

### Operating Context

A prototype that accepts user-provided receipt images, processes them, and presents extracted purchase information for review.

### Important Constraints

- Receipt image quality may affect extraction accuracy.
- Receipt layouts and formats may vary.
- Warranty duration may not appear on the receipt.
- External manufacturer warranty information may not be available.
- AI-generated information may be incorrect and requires appropriate validation.

### Explicit Out-of-Scope Tasks

- Guaranteeing correct extraction from every receipt.
- Automatically verifying every manufacturer's warranty policy.
- Making warranty claims or purchases on behalf of users.
- Presenting estimated warranty durations as confirmed manufacturer information.
- Providing legal decisions about warranty entitlement.

## 0.6 Evaluation Focus

The evaluation will determine whether WarrantyWise AI can extract and structure receipt information accurately, calculate warranty expiration dates correctly when sufficient information is available, and identify missing or uncertain information without presenting unsupported claims as facts.

# Section 1 — Functional Requirements

Functional requirements describe what the system must do.

| ID | Requirement — The system SHALL | Scope Boundary — SHALL NOT |
|---|---|---|
| FR1 | Allow users to upload receipt images in supported image formats. | Treat unsupported files as valid receipt images. |
| FR2 | Extract available purchase information, including product name, purchase date, price, and merchant name, from uploaded receipt images. | Assume that information missing from a receipt has been successfully extracted. |
| FR3 | Organise extracted purchase information into a predefined JSON structure. | Treat output that fails the required structure as valid structured data. |
| FR4 | Identify and mark fields that are missing, unclear, or uncertain. | Silently replace missing information with invented values. |
| FR5 | Calculate a warranty expiration date when a valid purchase date and a supported warranty duration are available. | Present an estimated warranty duration or expiration date as confirmed manufacturer information without supporting evidence. |
| FR6 | Display extracted purchase information and its uncertainty indicators for users to review. | Prevent users from recognising which information may be incorrect or incomplete. |

# Section 2 — Non-Functional Requirements

Non-functional requirements describe how well the system should perform. Each requirement includes a measurement method, metric, and proposed acceptance threshold.

| ID | Quality Attribute | Requirement | Measurement Method | Metric | Threshold |
|---|---|---|---|---|---|
| NFR1 | Extraction Accuracy | The system shall extract required purchase fields correctly from supported receipt images. | Compare extracted fields against manually verified reference data from at least 30 receipt images. | Field-level exact-match accuracy | At least 90% across evaluated fields |
| NFR2 | Performance | The system shall process a supported receipt image within the defined response-time target. | Measure end-to-end processing time across at least 30 test runs under the same test conditions. | 90th-percentile processing time (p90) | At most 10 seconds per receipt |
| NFR3 | Reliability | The system shall handle invalid or unreadable receipt images without an unhandled application error. | Test at least 10 invalid, unsupported, or unreadable image cases. | Percentage of test cases handled without an unhandled error | 100% of tested cases |
| NFR4 | Data Validation | The system shall produce JSON output that conforms to its predefined schema for successfully processed receipts. | Validate outputs from at least 30 test receipts against the JSON schema. | Percentage of outputs passing schema validation | At least 95% |

**Note:** These thresholds are proposed for the initial prototype. They are not measured results and may be adjusted if testing shows that the targets are unsuitable for the available data or implementation constraints.

# Section 3 — Responsible AI Requirements

Responsible AI requirements define behaviours and controls that reduce risks to users.

| ID | Responsible AI Risk | Requirement | Measurement Method | Metric | Threshold |
|---|---|---|---|---|---|
| RAI1 | Transparency and Uncertainty | The system shall clearly label missing or uncertain fields and distinguish estimated warranty information from information supported by available evidence. | Test at least 20 cases containing missing, unclear, or unsupported warranty information and inspect the output labels. | Percentage of test cases with appropriate uncertainty identification and labelling | 100% of tested cases |
| RAI2 | Privacy | The system shall not transmit receipt images or extracted personal information to external services without appropriate disclosure and user authorisation. | Inspect system data flows and outgoing requests during at least 10 privacy test cases. | Number of unauthorised external data transmissions | 0 |
| RAI3 | Human Oversight | The system shall allow users to review extracted purchase details before relying on the results. | Test the review workflow using at least 20 receipt cases, including cases with deliberately incorrect or incomplete extracted fields. | Percentage of tested cases in which results can be reviewed and errors or missing fields are made visible | 100% of tested cases |

**Note:** These are proposed acceptance thresholds. They must be verified through implementation and testing before the system can be considered compliant.

# Section 4 — Reflection

**Which Responsible AI requirement will be the most difficult to measure technically, and why?**

RAI1, Transparency and Uncertainty, will likely be the most difficult to measure. The system must determine whether extracted information is genuinely supported by the receipt and distinguish it from estimates or unsupported AI-generated information. This requires manually verified reference data and carefully designed test cases. A result may follow the required JSON structure while still containing an incorrect warranty duration. Therefore, structural validation alone is insufficient to measure whether the system communicates uncertainty correctly.


