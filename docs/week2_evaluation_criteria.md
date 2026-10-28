# Week 2: Evaluation Criteria

## 1. Purpose

This document explains how WarrantyWise AI will be tested to check whether it works correctly.

The evaluation will focus on three main areas:
- Accuracy of receipt information extraction
- Correct handling of missing information
- Processing speed

The thresholds below are targets, not actual test results.

## 2. Evaluation Criteria

| Requirement ID | Evaluation Criterion | Capability Bucket | Measurement Method | Metric | Target | Expected Outcome |
|---|---|---|---|---|---|---|
| FR2 / NFR1 | Receipt information accuracy | Domain-specific | Test 30 receipts and compare the results with manually checked information. | Field accuracy | At least 85% | Users can extract receipt information with less manual work. |
| FR3 / NFR4 | Correct JSON output | Instruction-following | Test 30 receipts and check whether the output follows the required JSON format. | Valid JSON outputs | At least 90% | Information is stored in a consistent format. |
| FR4 / RAI1 | Handling missing or unclear information | Generation | Test 10 receipts with missing or unclear information. Check whether the system identifies these cases correctly. | Correctly identified cases | 100% | Users are warned when information is uncertain. |
| NFR2 | Processing speed | Cost/latency | Measure the processing time for 20 receipt uploads. | Processing time | At most 10 seconds for 90% of tests | Users receive results without waiting too long. |

## 3. Testing Plan

The system will be tested using these steps:

1. Collect 30 receipt images.
2. Check the correct information manually.
3. Upload the receipts to WarrantyWise AI.
4. Compare the extracted information with the correct information.
5. Check the JSON output and missing-information warnings.
6. Record the processing time.
7. Compare the actual results with the targets.

These tests will be completed after the main system has been developed.

## 4. Limitations

The test results may depend on receipt image quality and layout.

WarrantyWise AI will not guarantee a warranty expiration date when the warranty duration cannot be confirmed from available information.

## 5. Reflection

**Which evaluation criterion is most important, and why?**

Correctly handling missing or unclear information is the most important criterion. The system should not guess information or show an unconfirmed warranty expiration date as a fact. This helps users understand when they need to check the information themselves.
