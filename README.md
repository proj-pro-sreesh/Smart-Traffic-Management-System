# 🚦 Smart Traffic Management System (AWS-based)

This project demonstrates an **IoT-enabled Smart Traffic Management System** that uses AWS services for real-time data collection, processing, image analysis, and visualization.

---

## 🏗️ Architecture

```
[IoT Devices Simulator] 
       ↓ MQTT
[AWS IoT Core] 
       ↓ Rule Action
[AWS Kinesis Data Stream] 
       ↓ Trigger
[AWS Lambda] → [Amazon DynamoDB]
                 ↓
            [Amazon QuickSight]
       ↘                 ↙
[S3 (Images)] → [Lambda + Rekognition]
       ↓
[Amazon SNS Alerts]
```

---

## 📁 Folder Structure

```
smart-traffic-management/
│
├── iot_simulator.py
├── lambda_process_data/
│   └── index.py
├── lambda_image_analysis/
│   └── index.py
├── dashboard/
│   └── quicksight_screenshots/
├── README.md
└── architecture_diagram.png
```

---

## ⚙️ AWS Services Used

- **AWS IoT Core** – Receive IoT telemetry data via MQTT.
- **AWS Kinesis Data Streams** – Stream IoT data to processing layer.
- **AWS Lambda** – Process data and analyze images.
- **Amazon DynamoDB** – Store structured traffic data.
- **Amazon S3** – Store images from traffic cameras.
- **Amazon Rekognition** – Detect vehicles and congestion from images.
- **Amazon QuickSight** – Visualize traffic analytics.
- **Amazon SNS** – Send alerts in case of accidents/congestion.

---

## 🚀 Setup Instructions

1. **Deploy IoT Simulator**
   - Run `iot_simulator.py` to publish sample telemetry data.

2. **Set Up AWS IoT Core**
   - Create IoT Thing, attach certificates, and configure MQTT topic rules.

3. **Configure Kinesis + Lambda**
   - Create Kinesis Data Stream.
   - Attach Lambda (`lambda_process_data/index.py`) as trigger to process and push to DynamoDB.

4. **Set Up S3 + Rekognition Lambda**
   - Upload images to S3 bucket.
   - Trigger `lambda_image_analysis/index.py` on new uploads to analyze using Rekognition.

5. **Configure QuickSight Dashboard**
   - Connect DynamoDB as a dataset source.
   - Create visualizations for live traffic data.

6. **Set Up SNS Alerts**
   - Configure SNS topic to send congestion/accident alerts from Lambda.

---

## 📌 Notes

- Make sure to configure proper IAM roles and permissions for each AWS service.
- All Lambda functions should have environment variables configured for their respective table/bucket/topic names.

---

## 👩‍💻 Author

Developed as part of a Smart City initiative demo.
