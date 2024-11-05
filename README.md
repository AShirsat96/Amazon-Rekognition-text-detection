# AWS Rekognition Text Detection

A Python implementation for detecting and extracting text from images using AWS Rekognition's text detection feature. This implementation analyzes images stored in S3 buckets and provides detailed information about detected text including confidence scores and hierarchical relationships.

## Prerequisites

- Python 3.8.8
- boto3 (AWS SDK for Python)
- AWS Account with Rekognition and S3 access
- AWS Access Key and Secret Access Key
- S3 bucket containing images to analyze

## Installation

Install the required AWS SDK for Python:

```bash
pip install boto3
```

## Configuration

You'll need to configure the following AWS credentials:

```python
aws_accesskey = <Your Access Key>
aws_secretaccess = <Your secret access key>
myregion = <your region>
```

## Required Libraries
```python
import boto3
```

## Usage

The main functionality is provided through the `DetectText_Image` function:

```python
DetectText_Image(aws_access, aws_secret, aws_region, bucket_name, photo_name)
```

### Parameters

- `aws_access`: Your AWS access key ID
- `aws_secret`: Your AWS secret access key
- `aws_region`: AWS region for Rekognition service
- `bucket_name`: Name of the S3 bucket containing the image
- `photo_name`: Name of the image file in the S3 bucket

### Return Value

Returns the total number of text detections found in the image (integer).

### Output Format

For each detected text element, the function prints:
- Detected text content
- Confidence score (percentage)
- Detection ID
- Parent ID (if applicable)
- Text type (LINE or WORD)

Example output:
```
Detected text
----------
Detected text: ROOTS 9
Confidence: 99.48%
Id: 0
Type: LINE

Detected text: Welcome
Confidence: 99.73%
Id: 5
Parent Id: 1
Type: WORD
```

## Example Usage

```python
# Analyze an image for text content
text_count = DetectText_Image(
    aws_accesskey,
    aws_secretaccess,
    myregion,
    'your-bucket-name',
    'image.jpg'
)
```

## Features

- Detects and extracts text from images
- Provides confidence scores for each detection
- Identifies text hierarchy (lines and words)
- Shows parent-child relationships between detected text elements
- Formats confidence scores to 2 decimal places
- Works with images stored in S3 buckets

## Text Detection Types

The API returns two types of text detections:
- `LINE`: Complete lines of text detected in the image
- `WORD`: Individual words within detected lines

## Notes on Results

- Each text detection includes a unique ID
- Words include a ParentId linking to their parent line
- Confidence scores indicate the API's certainty about the detection
- Results are ordered by detection type (LINES first, then WORDS)
