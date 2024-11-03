# Amazon Rekognition Text Detection 📷📝

A Python application that utilizes Amazon Rekognition's powerful OCR (Optical Character Recognition) capabilities to detect and extract text from images. This tool demonstrates AWS Rekognition's text detection features in a practical implementation.

## Overview

This project showcases the integration of Amazon Rekognition's text detection service to:
- Extract text from images
- Process multiple image formats
- Provide detailed text detection analysis including location and confidence scores
- Handle both local and S3-stored images

## Prerequisites

Before using this application, ensure you have:

1. **AWS Account Setup**:
   - An active AWS account
   - AWS credentials configured
   - Appropriate IAM permissions for Amazon Rekognition

2. **Required Software**:
   - Python 3.x
   - AWS CLI installed and configured
   - Required Python packages:
     ```bash
     pip install boto3 pillow
     ```

3. **AWS Credentials**:
   - Configure AWS credentials either through:
     - AWS CLI (`aws configure`)
     - Environment variables
     - AWS credentials file

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/AShirsat96/Amazon_Rekognition_Detect_Text_In_Image.git
   cd Amazon_Rekognition_Detect_Text_In_Image
   ```

2. Install required dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Configure AWS credentials if not already done:
   ```bash
   aws configure
   ```

## Usage

### Basic Usage

1. Run the script with your image:
   ```python
   python detect_text.py --image path/to/your/image.jpg
   ```

### Code Example

```python
import boto3

def detect_text(photo):
    client = boto3.client('rekognition')
    
    with open(photo, 'rb') as image:
        response = client.detect_text(Image={'Bytes': image.read()})
        
    textDetections = response['TextDetections']
    print('Detected text\n----------')
    for text in textDetections:
        print('Detected text:' + text['DetectedText'])
        print('Confidence: ' + "{:.2f}".format(text['Confidence']) + "%")
        print('Type:' + text['Type'])
        if 'ParentId' in text:
            print('Parent Id: ' + text['ParentId'])
        print('Id: {}'.format(text['Id']))
        print()
```

## Features

1. **Text Detection**:
   - Detects both printed and handwritten text
   - Provides confidence scores for detections
   - Identifies text location in images

2. **Output Information**:
   - Detected text content
   - Confidence levels
   - Text type (LINE/WORD)
   - Geometric information about text location

3. **Support for Multiple Image Sources**:
   - Local image files
   - Images in S3 buckets
   - Various image formats (JPEG, PNG, etc.)

## Project Structure

```
Amazon_Rekognition_Detect_Text_In_Image/
│
├── detect_text.py          # Main script for text detection
├── requirements.txt        # Project dependencies
├── examples/              # Example images and results
│   ├── sample_image.jpg
│   └── results/
└── README.md              # Project documentation
```

## Best Practices

1. **Image Quality**:
   - Use clear, well-lit images
   - Ensure text is clearly visible
   - Maintain good contrast between text and background

2. **Error Handling**:
   - Implement proper error handling for AWS service calls
   - Validate input images before processing
   - Check image size and format compatibility

3. **Security**:
   - Never commit AWS credentials
   - Use IAM roles with minimum required permissions
   - Implement secure handling of sensitive data

## Troubleshooting

Common issues and solutions:

1. **Authentication Errors**:
   - Verify AWS credentials are properly configured
   - Check IAM permissions for Rekognition services

2. **Image Processing Errors**:
   - Ensure image format is supported
   - Check image file size limits
   - Verify image file integrity

3. **Performance Issues**:
   - Optimize image size before processing
   - Consider batch processing for multiple images
   - Monitor AWS service quotas

## AWS Configuration

1. **Required IAM Permissions**:
   ```json
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Effect": "Allow",
               "Action": [
                   "rekognition:DetectText"
               ],
               "Resource": "*"
           }
       ]
   }
   ```

2. **AWS Region Configuration**:
   - Set your preferred AWS region in code or config
   - Consider latency when choosing regions


## Contact

Aniket Shirsat

Email: ashirsat96@gmail.com 

---
**Note**: 
- Costs may be incurred when using Amazon Rekognition services
- Review AWS pricing before processing large volumes of images
- Follow AWS best practices for production deployments
