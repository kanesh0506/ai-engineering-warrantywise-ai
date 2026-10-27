# Week 1 Project Scope: WarrantyWise AI

## 1. Project Title

WarrantyWise AI: AI-Powered Receipt Information Extraction and Warranty Tracking

## 2. Problem Statement

Consumers may lose purchase receipts, struggle to retrieve purchase information, or forget warranty expiration dates. Manually recording information from receipts can be inconvenient and time-consuming.

## 3. Engineering Problem

Receipt images contain unstructured text and may have different layouts, unclear characters, or missing information. Extracting text alone does not guarantee that the system correctly identifies and organises purchase details.

The engineering challenge is to develop an AI-assisted workflow that extracts receipt information, converts it into structured data, validates the results, and handles uncertainty appropriately.

## 4. Proposed Solution

WarrantyWise AI will process receipt images using OCR or a vision-based model and use AI to organise relevant information into structured fields.

The proposed output may include:

- Product name
- Purchase date
- Purchase price
- Store or merchant name
- Warranty duration, when available
- Estimated or confirmed warranty expiration date, depending on the available evidence

Missing or uncertain information will be marked accordingly instead of being presented as verified information.

## 5. Project Objectives

1. Extract relevant information from receipt images.
2. Organise extracted information into a predefined JSON structure.
3. Validate the structure and identify missing fields.
4. Calculate warranty expiration dates when sufficient information is available.
5. Evaluate the accuracy and limitations of the extraction process.

## 6. Initial Scope

### Included

- Receipt image input.
- OCR or vision-based text extraction.
- AI-assisted information structuring.
- JSON output and basic field validation.
- Basic warranty date calculation.
- Identification of missing or uncertain information.

### Excluded from the Initial Scope

- Automatic verification of every manufacturer's warranty policy.
- Direct integration with retailer databases.
- Large-scale commercial deployment.
- Guaranteed accuracy for every receipt format.

## 7. Proposed Evaluation

The prototype can be evaluated using a small collection of receipt images with manually checked reference information.

Possible evaluation criteria include:

- Correct extraction of product names and purchase dates.
- Accuracy of extracted prices and merchant names.
- Validity of the generated JSON structure.
- Correctness of warranty date calculations when the required inputs are known.
- Appropriate handling of missing, unclear, or uncertain information.

The evaluation dataset and results will be documented after testing. No performance results are claimed at this stage.

## 8. Expected Outcome

A prototype that demonstrates receipt information extraction, structured data generation, basic validation, and warranty tracking.

## 9. Key Limitations and Risks

- OCR may misread unclear or low-quality text.
- AI may assign incorrect meanings to extracted information.
- Receipt information may not include the warranty duration.
- Warranty estimates may differ from actual manufacturer terms.
- User review is necessary before relying on uncertain results.

