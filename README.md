# 🏷️ AWS Image Labels Generator — Amazon Rekognition

> Built as part of the **Tech with Lucy** AWS Beginner Projects Course

---

## 📌 Project Overview

This project uses **Amazon S3** and **Amazon Rekognition** to automatically detect and label objects, scenes, and concepts within images. An image is uploaded to an S3 bucket, Rekognition analyzes it, and returns labels with confidence scores.

---

## 🛠️ AWS Services Used

| Service | Purpose | Configuration |
|---|---|---|
| **Amazon S3** | Store images for analysis | Bucket: `aws-rekognition-label-images`, Region: `us-east-1` |
| **Amazon Rekognition** | Detect labels in images | Region: `us-east-1` |
| **AWS IAM** | User permissions | Policy: `AdministratorAccess` |

---

## 🚀 How It Works

```
Local Image
     ↓
Upload to S3 Bucket
(aws-rekognition-label-images)
     ↓
Amazon Rekognition API
(DetectLabels)
     ↓
Labels + Confidence Scores
     ↓
Console Output + labels_output.json
```

1. Image is uploaded to the S3 bucket `aws-rekognition-label-images`
2. Rekognition's `detect_labels` API analyzes the S3 image
3. Returns up to 10 labels with ≥75% confidence
4. Results printed to console and saved as JSON

---

## 📸 Screenshots

### S3 Bucket Setup
<img width="724" height="554" alt="image" src="https://github.com/user-attachments/assets/7189b14c-e8f3-471e-a163-ece352b2bb15" />

### IAM Permissions Setup
<img width="627" height="299" alt="image" src="https://github.com/user-attachments/assets/5cabd7a0-8171-41d8-adfa-e550d77a6621" />


---

## 💻 Sample Output

```
==================================================
  🏷️  AWS Image Labels Generator
  Amazon S3 + Amazon Rekognition
==================================================

⬆️  Uploading 'sample_image.jpg' to s3://aws-rekognition-label-images/sample_image.jpg ...
✅ Upload complete!

🔍 Analyzing image from s3://aws-rekognition-label-images/sample_image.jpg ...

📋 Detected Labels:
─────────────────────────────────────────────
   1. Dog                      99.21%
   2. Animal                   99.21%
   3. Pet                      98.50%
   4. Outdoors                 87.43%
   5. Nature                   82.10%
─────────────────────────────────────────────
  Total labels found: 5

💾 Labels saved to 'labels_output.json'
```

---

## ⚙️ Setup & Installation

### Prerequisites
- Python 3.8+
- AWS Account with IAM user (AdministratorAccess)
- AWS CLI installed and configured
- S3 bucket `aws-rekognition-label-images` created in `us-east-1`

### 1. Clone the repository
```bash
git clone https://github.com/YOUR_USERNAME/aws-image-labels-rekognition.git
cd aws-image-labels-rekognition
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Configure AWS credentials
```bash
aws configure
# AWS Access Key ID: <your key>
# AWS Secret Access Key: <your secret>
# Default region name: us-east-1
# Default output format: json
```

### 4. Run the project
```bash
python src/rekognition_labels.py
```

---

## 🔐 IAM Setup

In this project, the IAM user was configured with:
- **Permissions option:** Attach policies directly
- **Policy attached:** `AdministratorAccess` (AWS managed - job function)

> ⚠️ For production use, it's best practice to use a least-privilege policy (only `rekognition:DetectLabels` and `s3:PutObject`) instead of AdministratorAccess.

---

## 📁 Project Structure

```
aws-image-labels-rekognition/
├── README.md
├── requirements.txt
├── .gitignore
├── src/
│   └── rekognition_labels.py
└── screenshots/
    ├── s3-bucket-creation.png
    └── iam-permissions-setup.png
```

---

## 📚 What I Learned

- Creating and configuring an **Amazon S3 bucket** (General Purpose, us-east-1)
- Setting up **AWS IAM users** and attaching permission policies
- Using **boto3 SDK** to upload files to S3 programmatically
- Calling **Amazon Rekognition's DetectLabels API** via S3 integration
- Parsing and saving AWS API JSON responses

---

## 🔗 Resources

- [Amazon Rekognition Docs](https://docs.aws.amazon.com/rekognition/)
- [Amazon S3 Docs](https://docs.aws.amazon.com/s3/)
- [boto3 Rekognition Reference](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/rekognition.html)
- [Tech with Lucy Course](https://techwithlucy.com)
