# Week 3 — V1 Data Pipeline Decisions

## 1. Project Overview

**Project:** WarrantyWise AI  
**Selected data type:** Computer Vision / Images  
**Pipeline version:** week3-v1

The pipeline processes receipt images from the SROIE dataset. The prepared images will be used as input for future OCR and receipt information extraction tasks.

## 2. Data Source

- **Dataset:** SROIE Dataset
- **Source location:** `data/raw/sroie_datasetv2/`
- **Total receipt images:** 973
- **Image formats:** JPG and other supported image formats
- **Purpose:** Provide receipt images for testing and developing the receipt information extraction workflow.
- **Access rights:** Not verified. Dataset licensing and usage permissions must be checked before redistribution.

## 3. Part B Preparation Comparison

Two image preparation approaches were considered:

| Approach | Description | Decision |
|---|---|---|
| Resize to 224 × 224 | Convert images to RGB and resize to a fixed size | Not selected |
| Preserve original dimensions | Convert images to RGB without resizing | Selected |

The second approach was selected because receipt images contain small printed text. Preserving their original dimensions avoids unnecessary loss of text detail during resizing.

## 4. Selected Preparation Configuration

The following settings were used:

- Convert images to RGB.
- Save prepared images in PNG format.
- Preserve original image dimensions.
- Retain the relationship between each source image and its prepared output.

## 5. V1 Pipeline Stages

| Stage | Description |
|---|---|
| Ingest | Locate and load receipt images from the source folder and its subfolders. |
| Inspect | Verify that images can be opened and record their dimensions and colour modes. |
| Prepare | Convert images to RGB and save them as PNG files without resizing. |
| Validate | Check output existence, file size and SHA-256 fingerprints. |
| Record lineage | Save source hashes, output hashes and source-to-output mappings in the pipeline manifest. |

## 6. ETL / ELT Decision

The pipeline follows an ETL approach.

Receipt images are extracted from the source dataset, transformed into RGB PNG images, and then stored in the pipeline output directory.

## 7. Batch / Streaming Decision

Batch processing was selected because the SROIE dataset contains a fixed collection of 973 receipt images.

The pipeline processes the available images together rather than continuously processing incoming receipts.

## 8. Pipeline Output

Prepared images:

`data/pipeline_v1/images/`

Pipeline manifest:

`data/pipeline_v1/images/pipeline_manifest.json`

Part B lineage manifest:

`data/week3_manifest.json`

## 9. Pipeline Validation and Repeatability

The pipeline successfully processed 973 source images and generated 973 prepared images.

The repeatability test was successful:

- Source fingerprints matched.
- Prepared output fingerprints matched.
- Source-to-output mappings matched.

This confirms that repeated execution with the same inputs and configuration produced matching outputs.

## 10. Limitations and Risks

- The SROIE dataset contains receipt images but does not provide warranty duration or warranty expiry labels.
- The pipeline prepares images but does not perform OCR or warranty information extraction.
- Dataset licensing and access rights have not yet been verified.
- Image readability does not guarantee that all receipt text can be extracted correctly.

Further OCR, information extraction and warranty validation will be addressed in later development stages.
