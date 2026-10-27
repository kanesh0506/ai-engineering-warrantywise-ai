# WarrantyWise AI

**AI-powered receipt information extraction and warranty tracking**

## 1. Project Overview

WarrantyWise AI is a proposed AI-powered system that helps users extract important purchase information from receipts and organise warranty details. It aims to turn unstructured receipt information into structured data that users can review and track.

## 2. Problem Statement

Consumers may lose purchase receipts, have difficulty locating important purchase details, or forget when a product's warranty expires. Manually recording information from receipts can also be time-consuming.

## 3. Engineering Issue

Receipt images may contain unclear text, inconsistent layouts, missing information, or details that are difficult to interpret. An OCR system can extract text, but it may not reliably understand which information represents the product name, purchase date, price, or warranty duration.

An AI system must therefore extract relevant information, structure the results, handle uncertain fields, and avoid presenting unverified warranty information as fact.

## 4. Project Objectives

- Extract relevant purchase information from receipt images.
- Convert extracted information into structured JSON data.
- Identify missing or uncertain fields.
- Calculate warranty expiration dates when sufficient information is available.
- Distinguish verified information from estimates and assumptions.

## 5. Proposed Approach

The proposed system will use OCR or a vision-based model to process receipt images. An AI model will help identify and organise relevant purchase information into a predefined data structure.

The extracted information will be validated before it is used. When warranty duration is unavailable, the system will not automatically treat an estimated duration as a confirmed manufacturer warranty.

## 6. Initial Scope

The initial scope includes:

- Receipt image input.
- Purchase information extraction.
- Structured JSON output.
- Basic validation of extracted fields.
- Warranty expiration date calculation when the required information is available.
- Handling of missing or uncertain information.

Advanced integrations, automatic manufacturer warranty verification, and large-scale deployment are outside the initial scope.

## 7. Expected Outcome

The expected outcome is a prototype that demonstrates how AI can convert receipt images into structured purchase records and support basic warranty tracking.

The system's performance will depend on receipt image quality, text extraction accuracy, and the availability of reliable warranty information.

## 8. Limitations

- Poor-quality or damaged receipts may reduce extraction accuracy.
- AI-generated results may contain incorrect information.
- Warranty terms may vary by product, manufacturer, and purchase conditions.
- Estimated warranty durations must not be presented as confirmed facts.
- Users should be able to review extracted information before relying on it.

## 9. References

- Google Cloud Vision OCR Documentation: https://cloud.google.com/vision/docs/ocr
- Pydantic Documentation: https://docs.pydantic.dev/
- JSON Schema Getting Started Guide: https://json-schema.org/learn/getting-started-step-by-step

