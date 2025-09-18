

## 📄 `README.md`


# 🚦 Smart Traffic Management & Accident Alert System on AWS

## 📌 Overview
This project is a cloud-based solution to monitor real-time traffic conditions, detect accidents using IoT sensor data and image analysis, and alert authorities instantly.  
It integrates multiple AWS services to process live data, analyze accident images using AI (Rekognition), and display trends on an analytics dashboard.

---

## 👥 Team Members
- [Your Name] (Team Leader)
- [Member 2 Name]
- [Member 3 Name]

---

## 💡 Features
- Real-time vehicle sensor simulation using AWS IoT Core
- Data stream processing with Kinesis and Lambda
- Automatic accident detection from IoT data
- Image-based verification using Amazon Rekognition
- Storage of traffic and accident data in DynamoDB
- Emergency alerts using SNS (SMS/Email)
- Traffic trends dashboard with QuickSight

---

## 🏗️ Architecture
```

\[IoT Devices Simulator]
↓ MQTT
\[AWS IoT Core]
↓ Rule Action
\[AWS Kinesis Data Stream]
↓ Trigger
\[AWS Lambda] → \[Amazon DynamoDB]
↓
\[Amazon QuickSight]
↘                 ↙
\[S3 (Images)] → \[Lambda + Rekognition]
↓
\[Amazon SNS Alerts]

```

---

## 🧩 AWS Services Used
| Service            | Purpose                                |
|--------------------|------------------------------------------|
| AWS IoT Core        | Receive real-time sensor data from vehicles |
| Amazon Kinesis      | Stream and buffer high-volume data            |
| AWS Lambda          | Serverless backend processing                  |
| Amazon DynamoDB     | Store processed traffic and accident data      |
| Amazon S3            | Store uploaded accident images                  |
| Amazon Rekognition   | Detect accident severity from images            |
| Amazon SNS            | Send emergency SMS/email alerts                   |
| Amazon QuickSight     | Visualize live traffic & accident analytics      |
| AWS IAM                | Secure access control for services                 |

_All services are available under the AWS Free Tier limits._

---

## ⚙️ Setup Instructions

### 1. Prerequisites
- AWS Free Tier account
- AWS CLI installed and configured (`aws configure`)
- Node.js or Python installed
- IAM user with access to: IoT Core, Kinesis, Lambda, DynamoDB, S3, Rekognition, SNS, QuickSight

---

### 2. Create IoT Simulator
- In AWS IoT Core, create a **Thing** and download certificates
- Attach an IoT policy to allow `iot:Connect` and `iot:Publish`
- Write a Python script (`iot_simulator.py`) to send random traffic data via MQTT to your IoT Core endpoint

---

### 3. Stream & Process Data
- Create a **Kinesis Data Stream**
- Create an **IoT Rule** to forward data from IoT Core to the Kinesis stream
- Create a **Lambda function** to process each record:
  - Detect overspeed or sudden stop
  - Store data into **DynamoDB**

---

### 4. Accident Image Verification
- Create an **S3 bucket** for image uploads
- Configure **S3 Event Trigger** to call a Lambda function on image upload
- Lambda should:
  - Call **Amazon Rekognition** to detect damage or accidents
  - Update the corresponding accident entry in **DynamoDB**

---

### 5. Notifications
- Create an **SNS Topic** and **subscribe your phone/email**
- From Lambda, if an accident is confirmed, publish alert to SNS

---

### 6. Analytics Dashboard
- In **QuickSight**, connect to your DynamoDB table
- Create visualizations like:
  - Traffic volume by time
  - Accident heatmap by location
  - Weekly/Monthly accident trends

---

## ▶️ Running the Project
1. Start the `iot_simulator.py` script to push live data.
2. Upload accident images into the S3 bucket (optional testing).
3. Monitor DynamoDB for updates.
4. View live alerts via SMS/Email from SNS.
5. Explore dashboards in QuickSight.

---

## 📦 Folder Structure
```

smart-traffic-management/
│
├── iot\_simulator.py
├── lambda\_process\_data/
│   └── index.py
├── lambda\_image\_analysis/
│   └── index.py
├── dashboard/
│   └── quicksight\_screenshots/
├── README.md
└── architecture\_diagram.png

```

---

## 📊 Outcome
- Automated accident detection system using cloud services
- Real-time alerts for emergency response
- Traffic analysis dashboard for city planning
- Highly scalable, serverless architecture using AWS

---

## ⚠️ Notes
- Delete unused resources after testing to avoid charges.
- Rekognition has **5000 free images/month** in free tier.
- QuickSight has a **30-day free trial**.

---

## 🏁 Future Improvements
- Use real IoT sensors (GPS, accelerometer) instead of simulator
- Add live map visualization using Amazon Location Service
- Integrate ML models for traffic prediction

---

## 📜 License
MIT License

