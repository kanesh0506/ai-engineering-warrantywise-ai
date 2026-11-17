# Week 3 Data Inventory — WarrantyWise AI

## 1. Dataset selection

| Item | Details |
|---|---|
| Source ID | S01 |
| Dataset | SROIE Dataset v2 |
| Owner/uploader | urbikn |
| Source URL | https://www.kaggle.com/datasets/urbikn/sroie-datasetv2 |
| Data type | Unstructured image data with text annotations |
| Purpose | Receipt image inspection and preparation for the receipt information extraction task |
| Download method | KaggleHub |
| Download date (UTC) | 2026-11-17 |
| Retrieved version | Latest version available through KaggleHub at download time |
| Local raw path | `data/raw/sroie_datasetv2/` |
| Access and rights | Kaggle dataset page lists the licence as "Other (specified in description)". Check the dataset description and usage conditions before redistribution. |

## 2. Topic 2 requirement mapping

| Requirement | Data needed | Why this dataset is relevant | Limitation |
|---|---|---|---|
| Receipt image ingestion and inspection | Receipt images | Provides real receipt images for the image-processing pipeline | Image quality and layout may vary |
| Receipt information extraction | Receipt text and key-information annotations | Supports inspection of receipt text and selected labelled fields | Standard SROIE key-information labels do not provide warranty duration or expiry dates |

## 3. Ingestion evidence

- Downloaded dataset folder: `/content/week3_project/data/raw/sroie_datasetv2`
- Number of files found: 2925
- Number of image files found: 973
- Number of TXT files found: 1947

## 4. Representative image inspection

| Source ID | Image file | Image properties | Matching annotation files |
|---|---|---|---|
| S02 | `SROIE2019/test/img/X00016469670.jpg` | 463 × 894 px; RGB; JPEG | SROIE2019/test/box/X00016469670.txt, SROIE2019/test/entities/X00016469670.txt |
| S03 | `SROIE2019/test/img/X00016469671.jpg` | 463 × 776 px; RGB; JPEG | SROIE2019/test/box/X00016469671.txt, SROIE2019/test/entities/X00016469671.txt |

## 5. Initial observations

- The selected data pathway is Pathway C — Computer Vision / Images.
- Receipt images need to remain readable because small printed text is important for receipt information extraction.
- Image dimensions and colour modes should be inspected before selecting a resize or conversion method.
- Annotation files should be inspected to understand which receipt fields are actually labelled.
- Warranty duration and warranty expiry are not standard SROIE labels. They cannot be directly evaluated using this dataset alone.

## 6. Storage plan

- Raw source data: `data/raw/sroie_datasetv2/`
- Prepared images: `data/processed/`
- Image preparation manifest: `data/processed/image_manifest.csv`

The raw dataset is not included in the public GitHub repository.
