# คู่มือปฏิบัติการ (LAB Manual)
# วิชา ICT 24267 Cloud Computing
## ภาคการศึกษา 2/2568

---

| รายละเอียด | ข้อมูล |
|---|---|
| **รหัสวิชา** | ICT 24267 |
| **ชื่อวิชา** | Cloud Computing |
| **ผู้สอน** | อาจารย์อำนาจ คงเจริญถิ่น |
| **ภาคการศึกษา** | 2/2568 |
| **แพลตฟอร์ม** | Amazon Web Services (AWS) Free Tier |
| **ภาษาที่ใช้เขียนโปรแกรม** | Python 3.x (หลัก) |

---

## 📑 สารบัญ

### ส่วนนำ
- [📋 ภาพรวมคู่มือ LAB](#-ภาพรวมคู่มือ-lab)
- [🆓 AWS Free Tier ที่ใช้ในคู่มือนี้ (2026)](#-aws-free-tier-ที่ใช้ในคู่มือนี้-2026)
- [⚙️ การเตรียมความพร้อมก่อนเริ่ม LAB](#️-การเตรียมความพร้อมก่อนเริ่ม-lab)

---

### 📅 Week 1 — EC2 Advanced: Web Server & Python Flask Application
- [วัตถุประสงค์การเรียนรู้](#-week-1-ec2-advanced--web-server--python-flask-application)
- [LAB 1-1: สร้าง EC2 Instance พร้อม User Data](#-lab-1-1-สร้าง-ec2-instance-พร้อม-user-data)
  - ขั้นตอนที่ 1: สร้าง Key Pair
  - ขั้นตอนที่ 2: สร้าง Security Group
  - ขั้นตอนที่ 3: Launch EC2 Instance พร้อม User Data Script
  - ขั้นตอนที่ 4: เชื่อมต่อผ่าน SSH
  - ขั้นตอนที่ 5: ทดสอบ API
- [LAB 1-2: ติดตั้ง Nginx เป็น Reverse Proxy](#-lab-1-2-ติดตั้ง-nginx-เป็น-reverse-proxy)
- [LAB 1-3: จัดการ Elastic IP](#-lab-1-3-จัดการ-elastic-ip)
- [📝 แบบฝึกหัด Week 1](#-แบบฝึกหัด-week-1)
  - แบบฝึกหัดที่ 1: เพิ่ม Endpoint ใหม่ (PUT / DELETE)
  - แบบฝึกหัดที่ 2: Monitoring ด้วย CloudWatch
  - คำถามท้ายบท (5 ข้อ)

---

### 📅 Week 2 — RDS: Relational Database Service
- [วัตถุประสงค์การเรียนรู้](#-week-2-rds--relational-database-service)
- [LAB 2-1: สร้าง RDS MySQL Instance](#-lab-2-1-สร้าง-rds-mysql-instance)
  - ขั้นตอนที่ 1: สร้าง Security Group สำหรับ RDS
  - ขั้นตอนที่ 2: สร้าง RDS Instance
  - ขั้นตอนที่ 3: บันทึก Endpoint
- [LAB 2-2: ติดตั้ง MySQL Client และทดสอบการเชื่อมต่อ](#-lab-2-2-ติดตั้ง-mysql-client-และทดสอบการเชื่อมต่อ)
  - สร้าง Database, Tables และ Insert ข้อมูลตัวอย่าง
- [LAB 2-3: อัปเดต Flask App ให้ใช้ RDS](#-lab-2-3-อัปเดต-flask-app-ให้ใช้-rds)
  - สร้างไฟล์ `.env` และ `database.py`
  - อัปเดต `app.py` ให้รองรับ CRUD เต็มรูปแบบ
  - Endpoints: Students, Courses, Statistics
- [📝 แบบฝึกหัด Week 2](#-แบบฝึกหัด-week-2)
  - แบบฝึกหัดที่ 1: Enrollment System
  - แบบฝึกหัดที่ 2: RDS Snapshot
  - คำถามท้ายบท (5 ข้อ)

---

### 📅 Week 3 — Lambda & API Gateway: Serverless API
- [วัตถุประสงค์การเรียนรู้](#-week-3-lambda--api-gateway--serverless-api)
- [LAB 3-1: สร้าง IAM Role สำหรับ Lambda](#-lab-3-1-สร้าง-iam-role-สำหรับ-lambda)
- [LAB 3-2: สร้าง Lambda Layer สำหรับ PyMySQL](#-lab-3-2-สร้าง-lambda-layer-สำหรับ-pymysql)
- [LAB 3-3: สร้าง Lambda Functions](#-lab-3-3-สร้าง-lambda-functions)
  - Function 1: `ict24267-get-students` (GET)
  - Function 2: `ict24267-manage-students` (POST / PUT / DELETE)
- [LAB 3-4: สร้าง API Gateway](#-lab-3-4-สร้าง-api-gateway)
  - ขั้นตอนที่ 1: สร้าง REST API
  - ขั้นตอนที่ 2: สร้าง Resources และ Methods
  - ขั้นตอนที่ 3: Deploy API
  - ขั้นตอนที่ 4: ทดสอบ API ด้วย curl
- [LAB 3-5: Lambda สำหรับงาน Scheduled (EventBridge)](#-lab-3-5-lambda-สำหรับงาน-scheduled-cloudwatch-events)
  - Function: `lambda_daily_report.py`
  - ตั้ง Schedule ด้วย EventBridge
- [📝 แบบฝึกหัด Week 3](#-แบบฝึกหัด-week-3)
  - แบบฝึกหัดที่ 1: เพิ่ม Lambda Function ค้นหานักศึกษา
  - แบบฝึกหัดที่ 2: API Gateway Throttling
  - คำถามท้ายบท (5 ข้อ)

---

### 📅 Week 4 — Integration, Security & Monitoring
- [วัตถุประสงค์การเรียนรู้](#-week-4-integration-security--monitoring)
- [LAB 4-1: Secrets Manager / SSM Parameter Store](#-lab-4-1-secrets-manager-สำหรับ-database-credentials)
  - สร้าง SecureString Parameters ด้วย AWS CLI
  - อัปเดต Lambda ให้ดึง Credentials จาก SSM
- [LAB 4-2: CloudWatch Dashboard และ Alarms](#-lab-4-2-cloudwatch-dashboard-และ-alarms)
  - Dashboard: EC2 CPU, Lambda Invocations, API Gateway, RDS Connections
  - Alarms: High CPU Alert, Lambda Error Alert
- [LAB 4-3: สร้าง Frontend HTML สำหรับ Student System](#-lab-4-3-สร้าง-frontend-html-สำหรับ-student-system)
  - HTML + JavaScript Frontend เชื่อมต่อ API Gateway
  - ตั้งค่า Nginx ให้ Serve Frontend
- [LAB 4-4: Architecture Diagram และ Cost Estimation](#-lab-4-4-architecture-diagram-และ-cost-estimation)
  - สรุป Architecture ทั้งระบบ
  - ตาราง Free Tier Cost Estimation
- [LAB 4-5: Cleanup — ป้องกันค่าใช้จ่ายหลังสิ้นสุด LAB](#-lab-4-5-cleanup--ป้องกันค่าใช้จ่ายหลังสิ้นสุด-lab)
- [📝 แบบฝึกหัด Week 4](#-แบบฝึกหัด-week-4)
  - แบบฝึกหัดที่ 1: เพิ่ม API Key Authentication
  - แบบฝึกหัดที่ 2: CloudWatch Logs Insights
  - คำถามท้ายบท (5 ข้อ)
    
---

### 📚 ภาคผนวก
- [A. คำสั่ง AWS CLI ที่ใช้บ่อย](#a-คำสั่ง-aws-cli-ที่ใช้บ่อย)
- [B. Free Tier Checklist](#b-สรุป-free-tier-checklist)
- [C. Resources เพิ่มเติม](#c-resources-เพิ่มเติม)

---

## 📋 ภาพรวมคู่มือ LAB

คู่มือนี้ออกแบบเป็น **โปรเจกต์ต่อเนื่อง 4 สัปดาห์** โดยจะสร้าง **ระบบบันทึกข้อมูลนักศึกษา (Student Record System)** บน AWS Cloud แบบครบวงจร ตั้งแต่ EC2, RDS, Lambda และ API Gateway

```
โปรเจกต์หลัก: Student Record System on AWS
─────────────────────────────────────────────────────────
Week 1 │ EC2 Advanced  │ Web Server + Python Flask App
Week 2 │ RDS           │ MySQL Database + เชื่อมต่อ EC2
Week 3 │ Lambda + API  │ Serverless API สำหรับ CRUD
Week 4 │ Integration   │ รวมทุกส่วน + Security + Monitoring
─────────────────────────────────────────────────────────
```

> ⚠️ **ข้อสำคัญ**: LAB ทั้งหมดใช้เฉพาะ **AWS Free Tier** เท่านั้น นักศึกษาต้องระวังไม่ให้เกิดค่าใช้จ่าย โปรดอ่านส่วน "ข้อควรระวัง Free Tier" ในแต่ละ LAB อย่างละเอียด

---

## 🆓 AWS Free Tier ที่ใช้ในคู่มือนี้ (2026)

| บริการ | Free Tier Limit | หมายเหตุ |
|---|---|---|
| **EC2** | t3.micro, 750 ชม./เดือน | 12 เดือนแรก |
| **RDS** | db.t3.micro, 750 ชม./เดือน, 20 GB storage | 12 เดือนแรก |
| **Lambda** | 1,000,000 requests/เดือน, 400,000 GB-sec | ตลอดไป (Always Free) |
| **API Gateway** | 1,000,000 REST API calls/เดือน | 12 เดือนแรก |
| **S3** | 5 GB storage, 20,000 GET, 2,000 PUT | 12 เดือนแรก |
| **CloudWatch** | 10 metrics, 10 alarms, 1 million API requests | ตลอดไป (Always Free) |
| **IAM** | ไม่มีค่าใช้จ่าย | ตลอดไป |

---

## ⚙️ การเตรียมความพร้อมก่อนเริ่ม LAB

### 1. สร้าง AWS Account
1. ไปที่ https://aws.amazon.com/free/
2. คลิก **"Create a Free Account"**
3. กรอกข้อมูล Email, Password, Account Name
4. เลือก **Personal Account**
5. ใส่ข้อมูลบัตรเครดิต (สำหรับยืนยันตัวตน — จะไม่ถูกเรียกเก็บหากใช้งานใน Free Tier)
6. เลือก **Free Basic Support Plan**

### 2. ตั้งค่า Billing Alert (สำคัญมาก!)
1. ไปที่ **AWS Console → Billing → Budgets**
2. คลิก **"Create Budget"** → **"Use a template"**
3. เลือก **"Zero spend budget"**
4. ใส่ Email เพื่อรับแจ้งเตือน
5. คลิก **Create Budget**

> 💡 **แนะนำ**: ตั้ง Alert ที่ $0.01 เพื่อให้ระบบแจ้งเตือนทันทีที่มีค่าใช้จ่ายเกิดขึ้น

### 3. เครื่องมือที่ต้องติดตั้งในเครื่อง (Local)
```bash
# ตรวจสอบ Python version (ต้องการ 3.8+)
python --version

# ติดตั้ง AWS CLI v2
# Windows: ดาวน์โหลดจาก https://awscli.amazonaws.com/AWSCLIV2.msi
# macOS:
brew install awscli

# Linux:
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install

# ตรวจสอบ AWS CLI
aws --version
```

### 4. Region ที่แนะนำ
ใช้ **ap-southeast-1 (Singapore)** หรือ **us-east-1 (N. Virginia)** เพื่อ latency ที่ดีและครอบคลุม Free Tier ครบ

---

---

# 📅 WEEK 1: EC2 Advanced — Web Server & Python Flask Application

## วัตถุประสงค์การเรียนรู้
- ทบทวนและเพิ่มทักษะการสร้าง EC2 Instance
- ติดตั้งและ configure Python Flask Web Application บน EC2
- ทำความเข้าใจ Security Groups, Key Pairs, และ Elastic IP
- ใช้ User Data Script เพื่อ automate การติดตั้ง

## ระยะเวลา: 3 ชั่วโมง

---

## 🔧 LAB 1-1: สร้าง EC2 Instance พร้อม User Data

### ข้อควรระวัง Free Tier
- ✅ ใช้ **t3.micro** เท่านั้น
- ✅ **Amazon Linux 2023** หรือ **Ubuntu 22.04 LTS** (Free Tier eligible)
- ✅ Storage: **8 GB gp2/gp3** (ไม่เกิน 30 GB รวม)
- ❌ **อย่า** สร้าง Instance หลายตัวพร้อมกัน (750 ชม./เดือน รวมทุก Instance)

### ขั้นตอนที่ 1: สร้าง Key Pair
1. AWS Console → **EC2** → **Key Pairs** → **Create key pair**
2. Name: `ict24267-key`
3. Key pair type: **RSA**
4. Private key file format: **.pem** (macOS/Linux) หรือ **.ppk** (Windows + PuTTY)
5. คลิก **Create key pair** → บันทึกไฟล์ไว้ในที่ปลอดภัย

### ขั้นตอนที่ 2: สร้าง Security Group
1. EC2 → **Security Groups** → **Create security group**
2. Name: `ict24267-web-sg`
3. Description: `Security group for ICT24267 web server`
4. เพิ่ม **Inbound rules**:

| Type | Protocol | Port | Source | Purpose |
|---|---|---|---|---|
| SSH | TCP | 22 | 0.0.0.0/0 | Remote access |
| HTTP | TCP | 80 | 0.0.0.0/0 | Web access |
| Custom TCP | TCP | 5000 | 0.0.0.0/0 | Flask dev server |

### ขั้นตอนที่ 3: Launch EC2 Instance พร้อม User Data Script
1. EC2 → **Instances** → **Launch instances**
2. Name: `ict24267-webserver`
3. AMI: **Amazon Linux 2023 AMI** (Free tier eligible)
4. Instance type: **t3.micro** ✅
5. Key pair: `ict24267-key`
6. Security group: `ict24267-web-sg`
7. Storage: **8 GiB gp3**
8. เปิด **Advanced details** → **User data** → วางโค้ดนี้:

```bash
#!/bin/bash
# User Data Script - ICT24267 Week 1
yum update -y
yum install -y python3 python3-pip git

# ติดตั้ง Flask และ dependencies
pip3 install flask flask-cors boto3

# สร้างโฟลเดอร์โปรเจกต์
mkdir -p /home/ec2-user/student-app
cd /home/ec2-user/student-app

# สร้าง Flask Application เริ่มต้น
cat > app.py << 'APPEOF'
from flask import Flask, jsonify, request
from datetime import datetime

app = Flask(__name__)

# In-memory storage (Week 1 - ยังไม่มี Database)
students = [
    {"id": 1, "name": "สมชาย ใจดี", "student_id": "6401001", "gpa": 3.5},
    {"id": 2, "name": "สมหญิง รักเรียน", "student_id": "6401002", "gpa": 3.8},
]

@app.route('/')
def index():
    return jsonify({
        "message": "🎓 Student Record System - Week 1",
        "course": "ICT 24267 Cloud Computing",
        "semester": "2/2568",
        "server_time": datetime.now().strftime("%Y-%m-%d %H:%M:%S"),
        "version": "1.0.0"
    })

@app.route('/students', methods=['GET'])
def get_students():
    return jsonify({
        "status": "success",
        "count": len(students),
        "data": students
    })

@app.route('/students/<int:student_id>', methods=['GET'])
def get_student(student_id):
    student = next((s for s in students if s["id"] == student_id), None)
    if student:
        return jsonify({"status": "success", "data": student})
    return jsonify({"status": "error", "message": "Student not found"}), 404

@app.route('/students', methods=['POST'])
def add_student():
    data = request.get_json()
    new_student = {
        "id": len(students) + 1,
        "name": data.get("name"),
        "student_id": data.get("student_id"),
        "gpa": data.get("gpa", 0.0)
    }
    students.append(new_student)
    return jsonify({"status": "success", "data": new_student}), 201

@app.route('/health')
def health():
    return jsonify({"status": "healthy", "timestamp": datetime.now().isoformat()})

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000, debug=True)
APPEOF

chown -R ec2-user:ec2-user /home/ec2-user/student-app

# สร้าง systemd service เพื่อให้ app ทำงานอัตโนมัติ
cat > /etc/systemd/system/student-app.service << 'SVCEOF'
[Unit]
Description=Student Record System Flask App
After=network.target

[Service]
User=ec2-user
WorkingDirectory=/home/ec2-user/student-app
ExecStart=/usr/bin/python3 app.py
Restart=always
RestartSec=3

[Install]
WantedBy=multi-user.target
SVCEOF

systemctl daemon-reload
systemctl enable student-app
systemctl start student-app

echo "Setup complete!" >> /var/log/user-data.log
```

9. คลิก **Launch instance**

### ขั้นตอนที่ 4: เชื่อมต่อผ่าน Web Console

1. EC2 → **Instances** → **Launch instances**
2. Name: `ict24267-webserver`
3. Connect > Connect using Public IP > Connect

### ขั้นตอนที่ 5: ทดสอบ API
```bash
# ทดสอบจากภายใน EC2
curl http://localhost:5000/
curl http://localhost:5000/students
curl http://localhost:5000/health

# ทดสอบจากภายนอก (ใช้ Public IP)
curl http://<YOUR_PUBLIC_IP>:5000/
curl http://<YOUR_PUBLIC_IP>:5000/students

# เพิ่มนักศึกษาใหม่
curl -X POST http://<YOUR_PUBLIC_IP>:5000/students \
  -H "Content-Type: application/json" \
  -d '{"name": "สมศักดิ์ เก่งมาก", "student_id": "6401003", "gpa": 3.9}'
```

---

## 🔧 LAB 1-2: ติดตั้ง Nginx เป็น Reverse Proxy

```bash
# SSH เข้า EC2 แล้วรันคำสั่งต่อไปนี้
sudo yum install -y nginx

# ตั้งค่า Nginx
sudo tee /etc/nginx/conf.d/student-app.conf << 'EOF'
server {
    listen 80;
    server_name _;

    location / {
        proxy_pass http://127.0.0.1:5000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
EOF

# เริ่มต้น Nginx
sudo systemctl enable nginx
sudo systemctl start nginx

# ทดสอบ (Port 80 แล้ว)
curl http://<YOUR_PUBLIC_IP>/
curl http://<YOUR_PUBLIC_IP>/students
```

---

## 🔧 LAB 1-3: จัดการ Elastic IP

> ⚠️ **Elastic IP ฟรี** เฉพาะเมื่อ **Associated กับ Instance ที่กำลังรัน** เท่านั้น หาก Allocate แล้วไม่ได้ใช้จะมีค่าใช้จ่าย!

```
1. EC2 → Elastic IPs → Allocate Elastic IP address
2. คลิก Allocate
3. เลือก Elastic IP ที่ได้ → Actions → Associate Elastic IP
4. เลือก Instance: ict24267-webserver
5. คลิก Associate
```

หลังจากนี้ IP จะไม่เปลี่ยนแม้ Stop/Start Instance

---

## 📝 แบบฝึกหัด Week 1

### แบบฝึกหัดที่ 1: เพิ่ม Endpoint ใหม่
แก้ไขไฟล์ `app.py` บน EC2 เพื่อเพิ่ม Endpoint ต่อไปนี้:

```python
# TODO: สร้าง endpoint นี้ให้สมบูรณ์
@app.route('/students/<int:student_id>', methods=['PUT'])
def update_student(student_id):
    """
    อัปเดตข้อมูลนักศึกษาตาม ID
    Request body: {"name": "...", "gpa": ...}
    Response: ข้อมูลนักศึกษาที่อัปเดตแล้ว
    """
    # เขียนโค้ดของคุณที่นี่
    pass

@app.route('/students/<int:student_id>', methods=['DELETE'])
def delete_student(student_id):
    """
    ลบข้อมูลนักศึกษาตาม ID
    Response: {"status": "success", "message": "Student deleted"}
    """
    # เขียนโค้ดของคุณที่นี่
    pass
```

### แบบฝึกหัดที่ 2: Monitoring
1. ไปที่ **EC2 → Instances → เลือก Instance → Monitoring**
2. สังเกต Metrics ต่อไปนี้และบันทึกค่า:
   - CPU Utilization
   - Network In/Out
   - Status Check
3. ทดลอง stress test ด้วยคำสั่ง:
```bash
# ติดตั้ง stress tool
sudo yum install -y stress
# รัน CPU stress 60 วินาที
stress --cpu 1 --timeout 60
```
4. สังเกตการเปลี่ยนแปลง CPU Utilization ใน Console

### คำถามท้ายบท Week 1

1. **EC2 Instance Types**: t2.micro vs t3.micro ต่างกันอย่างไร? และทำไม AWS ถึงแนะนำ t3.micro สำหรับ workload ใหม่?

2. **Security Groups**: อธิบายความแตกต่างระหว่าง Inbound และ Outbound rules พร้อมยกตัวอย่างว่าทำไมการตั้งค่า Outbound ก็มีความสำคัญ

3. **User Data vs SSH**: เปรียบเทียบข้อดีข้อเสียของการ configure server ผ่าน User Data script กับการ SSH เข้าไปตั้งค่าเอง

4. **Elastic IP**: จากที่เรียนมา หากลืม Release Elastic IP ที่ไม่ได้ใช้งาน จะเกิดอะไรขึ้น? และต้องทำอย่างไรเพื่อหลีกเลี่ยงค่าใช้จ่าย?

5. **Flask Architecture**: อธิบายว่าทำไมถึงต้องใช้ Nginx เป็น Reverse Proxy หน้า Flask แทนที่จะให้ Flask รับ request โดยตรง

---

---

# 📅 WEEK 2: RDS — Relational Database Service

## วัตถุประสงค์การเรียนรู้
- สร้างและจัดการ RDS MySQL Instance บน AWS
- เชื่อมต่อ EC2 กับ RDS อย่างปลอดภัยผ่าน Private Subnet
- ปรับปรุง Flask Application ให้ใช้งาน Database จริง
- เข้าใจหลักการ Database Security ใน Cloud

## ระยะเวลา: 3 ชั่วโมง

---

## 🔧 LAB 2-1: สร้าง RDS MySQL Instance

### ข้อควรระวัง Free Tier
- ✅ Instance class: **db.t3.micro** เท่านั้น
- ✅ Storage: **20 GB** (ไม่เกิน 20 GB)
- ✅ เลือก **Single-AZ** (ไม่ใช่ Multi-AZ)
- ❌ **อย่า** เปิด **Multi-AZ** (มีค่าใช้จ่าย!)
- ❌ **อย่า** เปิด **Performance Insights** เกิน 7 วัน
- ✅ 750 ชั่วโมง/เดือน สำหรับ db.t3.micro

### ขั้นตอนที่ 1: สร้าง Security Group สำหรับ RDS
1. EC2 → Security Groups → Create security group
2. Name: `ict24267-rds-sg`
3. Inbound rules:

| Type | Protocol | Port | Source |
|---|---|---|---|
| MySQL/Aurora | TCP | 3306 | `ict24267-web-sg` (เลือก SG ของ EC2) |

> 💡 **Best Practice**: อนุญาตเฉพาะ EC2 Security Group เข้าถึง RDS — ไม่เปิดให้ Public

### ขั้นตอนที่ 2: สร้าง RDS Instance
1. AWS Console → **RDS** → **Create database**
2. ตั้งค่าดังนี้:

```
Creation method:   Standard create
Engine:            MySQL
Engine version:    MySQL 8.0.x (latest 8.0)
Templates:         Free tier ✅

DB instance identifier: ict24267-db
Master username:        admin
Master password:        ICT24267  (หรือกำหนดเอง)

DB instance class:      db.t3.micro ✅
Storage type:           gp2
Allocated storage:      20 GB ✅
Enable storage autoscaling: ❌ ปิด

Availability:           Single DB instance ✅ (ไม่ใช่ Multi-AZ)

VPC:                    Default VPC
Public access:          No ✅
VPC security group:     ict24267-rds-sg

Database name:          student_db
Backup retention:       1 day
Enable automated backups: ✅
```

3. คลิก **Create database** (ใช้เวลาประมาณ 5-10 นาที)

### ขั้นตอนที่ 3: บันทึก Endpoint
หลังจาก RDS พร้อมใช้งาน ให้บันทึก:
- **Endpoint**: `ict24267-db.xxxxxxxxxx.ap-southeast-1.rds.amazonaws.com`
- **Port**: 3306

---

## 🔧 LAB 2-2: ติดตั้ง MySQL Client และทดสอบการเชื่อมต่อ

```bash
# SSH เข้า EC2 ก่อน จากนั้นรันคำสั่ง
1 — Update packages
sudo dnf update -y


2 — Install MySQL Community repo
sudo dnf install -y https://dev.mysql.com/get/mysql84-community-release-el9-1.noarch.rpm


3 — Import GPG key
sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2023


4 — Install MySQL Server 8.4 (LTS)
sudo dnf install -y mysql-community-server


5 — Start & enable service
sudo systemctl start mysqld
sudo systemctl enable mysqld


6 — Get temp root password & secure
sudo grep 'temporary password' /var/log/mysqld.log
sudo mysql_secure_installation


7 — ตรวจสอบ version
mysql --version

# ทดสอบเชื่อมต่อ RDS (แทนที่ด้วย Endpoint จริง)
mysql -h ict24267-db.xxxxxxxxxx.ap-southeast-1.rds.amazonaws.com \
      -u admin \
      -p

# เมื่อเข้าได้แล้ว สร้าง Database และ Tables
```

```sql
-- สร้าง Database
CREATE DATABASE IF NOT EXISTS student_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
USE student_db;

-- สร้างตาราง students
CREATE TABLE students (
    id INT AUTO_INCREMENT PRIMARY KEY,
    student_id VARCHAR(20) UNIQUE NOT NULL,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100),
    faculty VARCHAR(100),
    major VARCHAR(100),
    gpa DECIMAL(3,2) DEFAULT 0.00,
    enrollment_year INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

-- สร้างตาราง courses
CREATE TABLE courses (
    id INT AUTO_INCREMENT PRIMARY KEY,
    course_code VARCHAR(20) UNIQUE NOT NULL,
    course_name VARCHAR(200) NOT NULL,
    credits INT DEFAULT 3,
    instructor VARCHAR(100)
);

-- สร้างตาราง enrollments
CREATE TABLE enrollments (
    id INT AUTO_INCREMENT PRIMARY KEY,
    student_id INT,
    course_id INT,
    grade VARCHAR(2),
    semester VARCHAR(20),
    FOREIGN KEY (student_id) REFERENCES students(id),
    FOREIGN KEY (course_id) REFERENCES courses(id)
);

-- ใส่ข้อมูลตัวอย่าง
INSERT INTO students (student_id, name, email, faculty, major, gpa, enrollment_year) VALUES
('6401001', 'สมชาย ใจดี', 'somchai@example.com', 'ICT', 'Computer Science', 3.50, 2564),
('6401002', 'สมหญิง รักเรียน', 'somying@example.com', 'ICT', 'Information Technology', 3.80, 2564),
('6401003', 'สมศักดิ์ เก่งมาก', 'somsak@example.com', 'ICT', 'Digital Innovation', 3.90, 2564);

INSERT INTO courses (course_code, course_name, credits, instructor) VALUES
('ICT24267', 'Cloud Computing', 3, 'อ.อำนาจ คงเจริญถิ่น'),
('ICT24101', 'Introduction to Programming', 3, 'อ.สมชาย วิทยาการ');

-- ดูข้อมูลที่เพิ่ม
SELECT * FROM students;
SELECT * FROM courses;

EXIT;
```

---

## 🔧 LAB 2-3: อัปเดต Flask App ให้ใช้ RDS

```bash
# ติดตั้ง Python MySQL connector บน EC2
pip3 install pymysql sqlalchemy flask-sqlalchemy python-dotenv
```

### สร้างไฟล์ `.env` สำหรับเก็บ credentials
```bash
cat > /home/ec2-user/student-app/.env << 'EOF'
DB_HOST=ict24267-db.xxxxxxxxxx.ap-southeast-1.rds.amazonaws.com
DB_PORT=3306
DB_NAME=student_db
DB_USER=admin
DB_PASSWORD=ICT24267
SECRET_KEY=ict24267-secret-key-2568
EOF

chmod 600 /home/ec2-user/student-app/.env
```

### สร้างไฟล์ `database.py`
```python
cat > /home/ec2-user/student-app/database.py << 'EOF'
import pymysql
import os
from dotenv import load_dotenv

load_dotenv()

def get_connection():
    """สร้าง Database Connection"""
    return pymysql.connect(
        host=os.getenv('DB_HOST'),
        port=int(os.getenv('DB_PORT', 3306)),
        database=os.getenv('DB_NAME'),
        user=os.getenv('DB_USER'),
        password=os.getenv('DB_PASSWORD'),
        charset='utf8mb4',
        cursorclass=pymysql.cursors.DictCursor
    )

def execute_query(query, params=None, fetch=True):
    conn = get_connection()
    try:
        with conn.cursor() as cursor:
            cursor.execute(query, params or ())
            if fetch:
                return cursor.fetchall()
            else:
                conn.commit()
                return cursor.lastrowid
    except Exception as e:
        conn.rollback()
        raise e
    finally:
        conn.close()
EOF
```

### อัปเดตไฟล์ `app.py` หลัก
```python
cat > /home/ec2-user/student-app/app.py << 'APPEOF'
from flask import Flask, jsonify, request
from datetime import datetime
import os
from dotenv import load_dotenv
from database import execute_query, get_connection

load_dotenv()

app = Flask(__name__)

@app.route('/')
def index():
    return jsonify({
        "message": "Student Record System - Week 2 (with RDS)",
        "course": "ICT 24267 Cloud Computing",
        "semester": "2/2568",
        "server_time": datetime.now().strftime("%Y-%m-%d %H:%M:%S"),
        "version": "2.0.0",
        "database": "MySQL RDS"
    })

@app.route('/health')
def health():
    db_status = "disconnected"
    try:
        conn = get_connection()
        conn.close()
        db_status = "connected"
    except Exception as e:
        db_status = f"error: {str(e)}"
    return jsonify({
        "status": "healthy",
        "database": db_status,
        "timestamp": datetime.now().isoformat()
    })

@app.route('/students', methods=['GET'])
def get_students():
    try:
        faculty = request.args.get('faculty')
        min_gpa = request.args.get('min_gpa', type=float)
        query = "SELECT * FROM students WHERE 1=1"
        params = []
        if faculty:
            query += " AND faculty = %s"
            params.append(faculty)
        if min_gpa:
            query += " AND gpa >= %s"
            params.append(min_gpa)
        query += " ORDER BY student_id"
        students = execute_query(query, params)
        return jsonify({"status": "success", "count": len(students), "data": students})
    except Exception as e:
        return jsonify({"status": "error", "message": str(e)}), 500

@app.route('/students/<int:student_id>', methods=['GET'])
def get_student(student_id):
    try:
        result = execute_query("SELECT * FROM students WHERE id = %s", (student_id,))
        if result:
            return jsonify({"status": "success", "data": result[0]})
        return jsonify({"status": "error", "message": "Student not found"}), 404
    except Exception as e:
        return jsonify({"status": "error", "message": str(e)}), 500

@app.route('/students', methods=['POST'])
def create_student():
    try:
        data = request.get_json()
        for field in ['student_id', 'name']:
            if not data.get(field):
                return jsonify({"status": "error", "message": f"Missing required field: {field}"}), 400
        new_id = execute_query(
            """INSERT INTO students (student_id, name, email, faculty, major, gpa, enrollment_year)
               VALUES (%s, %s, %s, %s, %s, %s, %s)""",
            (data['student_id'], data['name'], data.get('email', ''),
             data.get('faculty', ''), data.get('major', ''),
             data.get('gpa', 0.00), data.get('enrollment_year', datetime.now().year + 543)),
            fetch=False
        )
        student = execute_query("SELECT * FROM students WHERE id = %s", (new_id,))
        return jsonify({"status": "success", "data": student[0]}), 201
    except Exception as e:
        return jsonify({"status": "error", "message": str(e)}), 500

@app.route('/students/<int:student_id>', methods=['PUT'])
def update_student(student_id):
    try:
        existing = execute_query("SELECT id FROM students WHERE id = %s", (student_id,))
        if not existing:
            return jsonify({"status": "error", "message": "Student not found"}), 404
        data = request.get_json()
        execute_query(
            """UPDATE students SET name=%s, email=%s, faculty=%s, major=%s, gpa=%s
               WHERE id=%s""",
            (data.get('name'), data.get('email'), data.get('faculty'),
             data.get('major'), data.get('gpa'), student_id),
            fetch=False
        )
        student = execute_query("SELECT * FROM students WHERE id = %s", (student_id,))
        return jsonify({"status": "success", "data": student[0]})
    except Exception as e:
        return jsonify({"status": "error", "message": str(e)}), 500

@app.route('/students/<int:student_id>', methods=['DELETE'])
def delete_student(student_id):
    try:
        execute_query("DELETE FROM students WHERE id = %s", (student_id,), fetch=False)
        return jsonify({"status": "success", "message": f"Student ID {student_id} deleted"})
    except Exception as e:
        return jsonify({"status": "error", "message": str(e)}), 500

@app.route('/courses', methods=['GET'])
def get_courses():
    courses = execute_query("SELECT * FROM courses ORDER BY course_code")
    return jsonify({"status": "success", "count": len(courses), "data": courses})

@app.route('/stats')
def get_stats():
    total = execute_query("SELECT COUNT(*) as count FROM students")[0]['count']
    avg_gpa = execute_query("SELECT AVG(gpa) as avg FROM students")[0]['avg']
    top_students = execute_query(
        "SELECT name, student_id, gpa FROM students ORDER BY gpa DESC LIMIT 3"
    )
    return jsonify({
        "status": "success",
        "data": {
            "total_students": total,
            "average_gpa": round(float(avg_gpa or 0), 2),
            "top_students": top_students
        }
    })

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000, debug=False)
APPEOF
```

```bash
# Restart service
sudo systemctl restart student-app

# ทดสอบ
curl http://localhost:5000/health
curl http://localhost:5000/students
curl http://localhost:5000/stats

# เพิ่มนักศึกษา
curl -X POST http://localhost:5000/students \
  -H "Content-Type: application/json" \
  -d '{
    "student_id": "6401004",
    "name": "วิไล มีแววดี",
    "email": "vilai@example.com",
    "faculty": "ICT",
    "major": "Cloud Technology",
    "gpa": 3.75,
    "enrollment_year": 2564
  }'
```

---

## 📝 แบบฝึกหัด Week 2

### แบบฝึกหัดที่ 1: Enrollment System
เขียน Python Script เพื่อทำงานกับตาราง `enrollments`:
```python
# TODO: เขียนฟังก์ชันต่อไปนี้ใน app.py
# 1. POST /enrollments - ลงทะเบียนนักศึกษาในวิชา
# 2. GET /students/<id>/courses - ดูวิชาที่นักศึกษาลงทะเบียน
# 3. GET /courses/<id>/students - ดูนักศึกษาในวิชา
```

### แบบฝึกหัดที่ 2: RDS Snapshot
1. ไปที่ **RDS → Databases → ict24267-db**
2. Actions → **Take snapshot**
3. Snapshot identifier: `ict24267-db-week2-backup`
4. ตรวจสอบ snapshot ที่ **RDS → Snapshots**

### คำถามท้ายบท Week 2

1. **RDS vs ติดตั้ง MySQL บน EC2**: อธิบายข้อดีของการใช้ RDS Managed Service เปรียบเทียบกับการติดตั้ง MySQL บน EC2 เองอย่างน้อย 3 ข้อ

2. **Security Best Practice**: ทำไมถึงตั้งค่า `Public access: No` สำหรับ RDS แล้วให้ EC2 เป็น gateway แทน? มีความเสี่ยงอะไรถ้าเปิด Public access?

3. **Connection Pooling**: ถ้า Application มีผู้ใช้พร้อมกัน 1,000 คน และแต่ละ request สร้าง connection ใหม่ทุกครั้ง จะเกิดปัญหาอะไร? และ Connection Pool แก้ปัญหาได้อย่างไร?

4. **Database Backup**: AWS RDS มีกลยุทธ์ backup กี่แบบ? แต่ละแบบต่างกันอย่างไร?

5. **SQL Injection**: จากโค้ด `database.py` ทำไมการใช้ Parameterized Query (`%s`) ถึงปลอดภัยกว่า String Formatting?

---

---

# 📅 WEEK 3: Lambda & API Gateway — Serverless API

## วัตถุประสงค์การเรียนรู้
- สร้าง Lambda Functions สำหรับงาน Serverless
- เชื่อมต่อ Lambda กับ RDS ผ่าน VPC
- สร้าง REST API ด้วย API Gateway แบบสมบูรณ์
- เข้าใจ Serverless Architecture และข้อดีข้อเสีย

## ระยะเวลา: 3 ชั่วโมง

> 💡 **Week 3 ภาพรวม**: เราจะสร้าง Serverless API คู่ขนานกับ Flask ที่ทำใน Week 1-2 โดยใช้ Lambda + API Gateway แทน EC2 ทุก code ในสัปดาห์นี้ **วาง (paste) ลงใน AWS Console ได้โดยตรง ไม่ต้องสร้างไฟล์ใดๆ**

---

## 🔧 LAB 3-1: สร้าง IAM Role สำหรับ Lambda

IAM Role คือ "ใบอนุญาต" ให้ Lambda เข้าถึง AWS Services ต่างๆ ได้

### ขั้นตอน (ทำครั้งเดียว ใช้ได้ทุก Function)

**1.** ไปที่ AWS Console → พิมพ์ **IAM** ในช่องค้นหา → คลิก **IAM**

**2.** เมนูซ้าย → **Roles** → คลิกปุ่ม **Create role**

**3.** หน้า "Select trusted entity":
   - เลือก **AWS service**
   - Use case: เลือก **Lambda**
   - คลิก **Next**

**4.** หน้า "Add permissions" — ค้นหาและเพิ่ม **3 policies** นี้ทีละอัน:

| ค้นหาคำว่า | เลือก Policy นี้ | หน้าที่ |
|---|---|---|
| `LambdaVPC` | `AWSLambdaVPCAccessExecutionRole` | เข้าถึง RDS ใน VPC ได้ |
| `LambdaBasic` | `AWSLambdaBasicExecutionRole` | เขียน Log ลง CloudWatch ได้ |
| `SSMReadOnly` | `AmazonSSMReadOnlyAccess` | อ่าน Password จาก SSM ได้ (ใช้ใน Week 4) |

   > ✅ ติ๊กถูกทั้ง 3 แล้วค่อยคลิก **Next**

**5.** หน้า "Name, review, and create":
   - Role name: `ict24267-lambda-role`
   - คลิก **Create role**

✅ **เสร็จแล้ว** — จะเห็น Role ใหม่ในรายการ

---

## 🔧 LAB 3-2: สร้าง Lambda Layer สำหรับ PyMySQL

Lambda ไม่มี library `pymysql` ติดมาให้ เราต้องสร้าง "Layer" (ชุด library เสริม) แนบเข้าไป

> 💡 **Layer คืออะไร?** เปรียบเหมือนการ pip install แต่ทำครั้งเดียวแล้วแชร์ใช้ได้หลาย Function

### ขั้นตอนที่ 1: สร้าง Layer Package บน EC2

SSH เข้า EC2 แล้วรันคำสั่งต่อไปนี้ทีละบรรทัด:

```bash
# สร้างโฟลเดอร์สำหรับ Layer
mkdir -p /home/ec2-user/lambda-layer/python

# Download pymysql ให้ตรงกับ Lambda (Amazon Linux, Python 3.11)
pip3 install pymysql \
    --platform manylinux2014_x86_64 \
    --python-version 3.11 \
    --only-binary=:all: \
    --target /home/ec2-user/lambda-layer/python/

# สร้างไฟล์ .zip
cd /home/ec2-user/lambda-layer
zip -r pymysql-layer.zip python/

# ตรวจสอบว่าไฟล์สร้างแล้ว
ls -lh pymysql-layer.zip
```

> ✅ ควรเห็นไฟล์ `pymysql-layer.zip` ขนาดประมาณ 200-300 KB

### ขั้นตอนที่ 2: Upload Layer ขึ้น AWS

**1.** AWS Console → ค้นหา **Lambda** → คลิก **Lambda**

**2.** เมนูซ้าย → **Layers** → คลิก **Create layer**

**3.** กรอกข้อมูล:
   - Name: `pymysql-layer`
   - Upload: คลิก **Upload a .zip file** → เลือกไฟล์ `pymysql-layer.zip`
     > หากไฟล์อยู่บน EC2 ให้ download มาก่อน หรือใช้วิธี upload ผ่าน S3 ก็ได้
   - Compatible runtimes: เลือก **Python 3.11**

**4.** คลิก **Create**

✅ **เสร็จแล้ว** — เห็น Layer พร้อมใช้งาน

---

## 🔧 LAB 3-3: สร้าง Lambda Function 1 — ดึงข้อมูล (GET)

Function นี้ทำหน้าที่: **ดึงรายชื่อนักศึกษาทั้งหมด** และ **ดึงนักศึกษาคนเดียวตาม ID**

### ขั้นตอนที่ 1: สร้าง Function

**1.** Lambda → **Functions** → คลิก **Create function**

**2.** เลือก **Author from scratch** แล้วกรอก:
   - Function name: `ict24267-get-students`
   - Runtime: **Python 3.11**
   - Architecture: **x86_64**

**3.** Permissions → เปิด **Change default execution role**:
   - เลือก **Use an existing role**
   - Existing role: `ict24267-lambda-role`

**4.** คลิก **Create function**

### ขั้นตอนที่ 2: วาง Code

**1.** ในหน้า Function → แท็บ **Code**

**2.** เห็น editor มีไฟล์ `lambda_function.py` — **คลิกที่ไฟล์นั้น**

**3.** **ลบ code เดิมทั้งหมด** แล้ว **วาง code นี้แทน**:

```python
import json
import pymysql
import os
import logging

logger = logging.getLogger()
logger.setLevel(logging.INFO)

def get_db_connection():
    return pymysql.connect(
        host=os.environ['DB_HOST'],
        port=int(os.environ.get('DB_PORT', 3306)),
        database=os.environ['DB_NAME'],
        user=os.environ['DB_USER'],
        password=os.environ['DB_PASSWORD'],
        charset='utf8mb4',
        cursorclass=pymysql.cursors.DictCursor,
        connect_timeout=10
    )

def build_response(status_code, body):
    return {
        "statusCode": status_code,
        "headers": {
            "Content-Type": "application/json",
            "Access-Control-Allow-Origin": "*"
        },
        "body": json.dumps(body, ensure_ascii=False, default=str)
    }

def lambda_handler(event, context):
    logger.info(f"Event: {json.dumps(event)}")

    path_params  = event.get('pathParameters') or {}
    query_params = event.get('queryStringParameters') or {}
    student_id   = path_params.get('id')
    faculty      = query_params.get('faculty')
    min_gpa      = query_params.get('min_gpa')

    conn = None
    try:
        conn = get_db_connection()
        with conn.cursor() as cursor:

            if student_id:
                # ---- GET /students/{id} ----
                cursor.execute("SELECT * FROM students WHERE id = %s", (student_id,))
                student = cursor.fetchone()
                if not student:
                    return build_response(404, {"status": "error", "message": f"ไม่พบนักศึกษา ID {student_id}"})
                student['gpa'] = float(student['gpa']) if student['gpa'] else 0.0
                return build_response(200, {"status": "success", "data": student})

            else:
                # ---- GET /students ----
                query  = "SELECT * FROM students WHERE 1=1"
                params = []
                if faculty:
                    query += " AND faculty = %s"
                    params.append(faculty)
                if min_gpa:
                    query += " AND gpa >= %s"
                    params.append(float(min_gpa))
                query += " ORDER BY student_id"
                cursor.execute(query, params)
                students = cursor.fetchall()
                for s in students:
                    s['gpa'] = float(s['gpa']) if s['gpa'] else 0.0
                return build_response(200, {"status": "success", "count": len(students), "data": students})

    except pymysql.Error as e:
        logger.error(f"DB Error: {str(e)}")
        return build_response(500, {"status": "error", "message": f"Database error: {str(e)}"})
    except Exception as e:
        logger.error(f"Error: {str(e)}")
        return build_response(500, {"status": "error", "message": "Internal server error"})
    finally:
        if conn:
            conn.close()
```

**4.** คลิกปุ่ม **Deploy** (สีส้ม มุมขวาบน)

### ขั้นตอนที่ 3: ตั้งค่า Environment Variables

**1.** แท็บ **Configuration** → เมนูซ้าย **Environment variables** → **Edit**

**2.** คลิก **Add environment variable** เพิ่ม **5 ค่า** ดังนี้:

| Key | Value |
|---|---|
| `DB_HOST` | endpoint RDS ของคุณ เช่น `ict24267-db.abc123.ap-southeast-1.rds.amazonaws.com` |
| `DB_PORT` | `3306` |
| `DB_NAME` | `student_db` |
| `DB_USER` | `admin` |
| `DB_PASSWORD` | `ICT24267@2568` |

**3.** คลิก **Save**

### ขั้นตอนที่ 4: ตั้งค่า VPC (เพื่อให้เข้าถึง RDS ได้)

**1.** แท็บ **Configuration** → เมนูซ้าย **VPC** → **Edit**

**2.** ตั้งค่า:
   - VPC: เลือก **Default VPC**
   - Subnets: **เลือกทุก subnet** ที่มี
   - Security groups: เลือก `ict24267-rds-sg`

**3.** คลิก **Save**

> ⚠️ การ save VPC จะใช้เวลา 1-2 นาที รอจนขึ้น "Successfully updated"

### ขั้นตอนที่ 5: เพิ่ม Layer

**1.** เลื่อนลงล่างสุดของหน้า Function → ส่วน **Layers** → คลิก **Add a layer**

**2.** เลือก **Custom layers** → เลือก `pymysql-layer` → Version: เลือกเลขล่าสุด

**3.** คลิก **Add**

### ขั้นตอนที่ 6: ทดสอบ Function

**1.** แท็บ **Test** → คลิก **Create new event**

**2.** Event name: `test-get-all` แล้วแทนที่ JSON ทั้งหมดด้วย:

```json
{
  "httpMethod": "GET",
  "pathParameters": null,
  "queryStringParameters": null
}
```

**3.** คลิก **Test**

**4.** ✅ ผลลัพธ์ที่ถูกต้อง — ควรเห็น `"status": "success"` และรายชื่อนักศึกษา

---

## 🔧 LAB 3-4: สร้าง Lambda Function 2 — จัดการข้อมูล (POST/PUT/DELETE)

Function นี้ทำหน้าที่: **เพิ่ม / แก้ไข / ลบ** นักศึกษา

### ขั้นตอนที่ 1: สร้าง Function

**1.** Lambda → **Functions** → **Create function**

**2.** กรอกข้อมูล:
   - Function name: `ict24267-manage-students`
   - Runtime: **Python 3.11**
   - Execution role: `ict24267-lambda-role` (เหมือนเดิม)

**3.** คลิก **Create function**

### ขั้นตอนที่ 2: วาง Code

ใน editor ของ `lambda_function.py` — **ลบ code เดิมทั้งหมด** แล้ว **วาง code นี้แทน**:

```python
import json
import pymysql
import os
import logging
from datetime import datetime

logger = logging.getLogger()
logger.setLevel(logging.INFO)

def get_db_connection():
    return pymysql.connect(
        host=os.environ['DB_HOST'],
        port=int(os.environ.get('DB_PORT', 3306)),
        database=os.environ['DB_NAME'],
        user=os.environ['DB_USER'],
        password=os.environ['DB_PASSWORD'],
        charset='utf8mb4',
        cursorclass=pymysql.cursors.DictCursor,
        connect_timeout=10
    )

def build_response(status_code, body):
    return {
        "statusCode": status_code,
        "headers": {
            "Content-Type": "application/json",
            "Access-Control-Allow-Origin": "*"
        },
        "body": json.dumps(body, ensure_ascii=False, default=str)
    }

def lambda_handler(event, context):
    logger.info(f"Event: {json.dumps(event)}")

    http_method = event.get('httpMethod', '')
    path_params = event.get('pathParameters') or {}
    student_id  = path_params.get('id')

    body = {}
    if event.get('body'):
        body = json.loads(event['body'])

    conn = None
    try:
        conn = get_db_connection()

        if http_method == 'POST':
            return create_student(conn, body)
        elif http_method == 'PUT' and student_id:
            return update_student(conn, student_id, body)
        elif http_method == 'DELETE' and student_id:
            return delete_student(conn, student_id)
        else:
            return build_response(400, {"status": "error", "message": "คำขอไม่ถูกต้อง"})

    except Exception as e:
        logger.error(f"Error: {str(e)}")
        return build_response(500, {"status": "error", "message": str(e)})
    finally:
        if conn:
            conn.close()


def create_student(conn, data):
    # ตรวจสอบ field บังคับ
    for field in ['student_id', 'name']:
        if not data.get(field):
            return build_response(400, {"status": "error", "message": f"กรุณากรอก {field}"})

    current_thai_year = datetime.now().year + 543

    with conn.cursor() as cursor:
        cursor.execute(
            """INSERT INTO students (student_id, name, email, faculty, major, gpa, enrollment_year)
               VALUES (%s, %s, %s, %s, %s, %s, %s)""",
            (
                data['student_id'], data['name'],
                data.get('email', ''), data.get('faculty', ''),
                data.get('major', ''), data.get('gpa', 0.00),
                data.get('enrollment_year', current_thai_year)
            )
        )
        conn.commit()
        new_id = cursor.lastrowid
        cursor.execute("SELECT * FROM students WHERE id = %s", (new_id,))
        student = cursor.fetchone()
        student['gpa'] = float(student['gpa']) if student['gpa'] else 0.0

    return build_response(201, {"status": "success", "data": student})


def update_student(conn, student_id, data):
    with conn.cursor() as cursor:
        # ตรวจสอบว่ามีนักศึกษา ID นี้จริง
        cursor.execute("SELECT id FROM students WHERE id = %s", (student_id,))
        if not cursor.fetchone():
            return build_response(404, {"status": "error", "message": "ไม่พบนักศึกษา"})

        cursor.execute(
            """UPDATE students SET name=%s, email=%s, faculty=%s, major=%s, gpa=%s
               WHERE id=%s""",
            (data.get('name'), data.get('email'),
             data.get('faculty'), data.get('major'),
             data.get('gpa'), student_id)
        )
        conn.commit()
        cursor.execute("SELECT * FROM students WHERE id = %s", (student_id,))
        student = cursor.fetchone()
        student['gpa'] = float(student['gpa']) if student['gpa'] else 0.0

    return build_response(200, {"status": "success", "data": student})


def delete_student(conn, student_id):
    with conn.cursor() as cursor:
        affected = cursor.execute("DELETE FROM students WHERE id = %s", (student_id,))
        conn.commit()

    if affected == 0:
        return build_response(404, {"status": "error", "message": "ไม่พบนักศึกษา"})

    return build_response(200, {"status": "success", "message": f"ลบนักศึกษา ID {student_id} แล้ว"})
```

**3.** คลิก **Deploy**

### ขั้นตอนที่ 3-5: ตั้งค่า Environment Variables, VPC และ Layer

> ✅ ทำเหมือน Function แรก (`ict24267-get-students`) **ทุกขั้นตอน** — ค่าทุกอย่างเหมือนกันทั้งหมด

### ขั้นตอนที่ 6: ทดสอบ Function

**1.** แท็บ **Test** → **Create new event** ชื่อ `test-post` ด้วย JSON นี้:

```json
{
  "httpMethod": "POST",
  "pathParameters": null,
  "body": "{\"student_id\": \"9999999\", \"name\": \"ทดสอบ ระบบ\", \"faculty\": \"ICT\", \"major\": \"Cloud\", \"gpa\": 3.5}"
}
```

**2.** คลิก **Test** — ✅ ควรเห็น `"status": "success"` และข้อมูลนักศึกษาที่เพิ่งเพิ่ม

---

## 🔧 LAB 3-5: สร้าง Lambda Function 3 — รายงานประจำวัน (Scheduled)

Function นี้ทำหน้าที่: **สรุปสถิติอัตโนมัติทุกวัน** โดยไม่ต้องมีคนกด

### ขั้นตอนที่ 1: สร้าง Function

**1.** Lambda → **Functions** → **Create function**

**2.** กรอก:
   - Function name: `ict24267-daily-report`
   - Runtime: **Python 3.11**
   - Execution role: `ict24267-lambda-role`

**3.** คลิก **Create function**

### ขั้นตอนที่ 2: วาง Code

**ลบ code เดิมทั้งหมด** แล้ว **วาง code นี้**:

```python
import json
import pymysql
import os
import logging
from datetime import datetime

logger = logging.getLogger()
logger.setLevel(logging.INFO)

def get_db_connection():
    return pymysql.connect(
        host=os.environ['DB_HOST'],
        port=int(os.environ.get('DB_PORT', 3306)),
        database=os.environ['DB_NAME'],
        user=os.environ['DB_USER'],
        password=os.environ['DB_PASSWORD'],
        charset='utf8mb4',
        cursorclass=pymysql.cursors.DictCursor
    )

def lambda_handler(event, context):
    logger.info("Daily report triggered")
    conn = None
    try:
        conn = get_db_connection()
        with conn.cursor() as cursor:
            cursor.execute("SELECT COUNT(*) as total FROM students")
            total = cursor.fetchone()['total']

            cursor.execute("SELECT AVG(gpa) as avg_gpa FROM students")
            avg_gpa = cursor.fetchone()['avg_gpa']

            cursor.execute("""
                SELECT faculty, COUNT(*) as count, AVG(gpa) as avg_gpa
                FROM students GROUP BY faculty ORDER BY count DESC
            """)
            by_faculty = cursor.fetchall()

            cursor.execute("""
                SELECT name, student_id, gpa FROM students
                ORDER BY gpa DESC LIMIT 5
            """)
            top_students = cursor.fetchall()

        report = {
            "report_date":    datetime.now().strftime("%Y-%m-%d"),
            "total_students": total,
            "average_gpa":    round(float(avg_gpa or 0), 2),
            "by_faculty": [
                {"faculty": r['faculty'], "count": r['count'],
                 "avg_gpa": round(float(r['avg_gpa'] or 0), 2)}
                for r in by_faculty
            ],
            "top_5_students": [
                {"name": s['name'], "student_id": s['student_id'], "gpa": float(s['gpa'])}
                for s in top_students
            ]
        }

        logger.info(f"Report: {json.dumps(report, ensure_ascii=False)}")
        return {"statusCode": 200, "body": json.dumps(report, ensure_ascii=False)}

    except Exception as e:
        logger.error(f"Error: {str(e)}")
        raise
    finally:
        if conn:
            conn.close()
```

**3.** คลิก **Deploy**

**4.** ตั้ง Environment Variables และ VPC เหมือน Function ก่อนหน้า แต่ **Function นี้ไม่ต้องเพิ่ม Layer** (pymysql ไม่ได้ใช้ใน daily report) — รอก่อน ดูว่า test ผ่านไหม ถ้า error `No module named pymysql` ให้เพิ่ม Layer เหมือนเดิม

### ขั้นตอนที่ 3: ตั้ง Schedule ให้รันทุกวัน

**1.** แท็บ **Configuration** → **Triggers** → **Add trigger**

**2.** ตั้งค่า:
   - Trigger source: **EventBridge (CloudWatch Events)**
   - Rule: **Create a new rule**
   - Rule name: `ict24267-daily-report`
   - Schedule expression: `cron(0 1 * * ? *)`
     > หมายความว่า: รันทุกวัน เวลา 01:00 UTC = **08:00 น. ของไทย**

**3.** คลิก **Add**

✅ ตั้งแต่นี้ Function จะรันอัตโนมัติทุกเช้า

---

## 🔧 LAB 3-6: สร้าง API Gateway

API Gateway คือ "ประตู" ที่รับ HTTP Request จาก Internet แล้วส่งต่อให้ Lambda

### ขั้นตอนที่ 1: สร้าง REST API

**1.** AWS Console → ค้นหา **API Gateway** → คลิก **API Gateway**

**2.** คลิก **Create API**

**3.** เลือก **REST API** (ไม่ใช่ Private) → คลิก **Build**

**4.** ตั้งค่า:
   - API name: `ict24267-student-api`
   - Endpoint Type: **Regional**

**5.** คลิก **Create API**

### ขั้นตอนที่ 2: สร้าง Resource `/students`

**1.** เมนูซ้าย → **Resources** → คลิก **Actions** → **Create Resource**

**2.** ตั้งค่า:
   - Resource Name: `students`
   - Resource Path: `students`
   - ✅ ติ๊ก **Enable API Gateway CORS**

**3.** คลิก **Create Resource**

### ขั้นตอนที่ 3: เพิ่ม Method GET บน `/students`

**1.** คลิกเลือก `/students` → **Actions** → **Create Method** → เลือก **GET** → คลิก ✓

**2.** ตั้งค่า:
   - Integration type: **Lambda Function**
   - Lambda Function: `ict24267-get-students`

**3.** คลิก **Save** → **OK** (อนุญาตให้เรียก Lambda)

### ขั้นตอนที่ 4: เพิ่ม Method POST บน `/students`

**1.** คลิกเลือก `/students` → **Actions** → **Create Method** → **POST** → ✓

**2.** Lambda Function: `ict24267-manage-students` → **Save** → **OK**

### ขั้นตอนที่ 5: สร้าง Resource `/students/{id}`

**1.** คลิกเลือก `/students` → **Actions** → **Create Resource**

**2.** ตั้งค่า:
   - Resource Name: `student`
   - Resource Path: **`{id}`** (ต้องมีวงเล็บปีกกา)
   - ✅ ติ๊ก **Enable API Gateway CORS**

**3.** คลิก **Create Resource**

### ขั้นตอนที่ 6: เพิ่ม Methods บน `/students/{id}`

เพิ่ม **3 methods** ทีละอัน โดยทั้งหมดชี้ไปที่ `ict24267-manage-students`:

| Method | Lambda Function |
|---|---|
| GET | `ict24267-get-students` |
| PUT | `ict24267-manage-students` |
| DELETE | `ict24267-manage-students` |

> วิธีเพิ่มแต่ละ method: คลิก `{id}` → Actions → Create Method → เลือก Method → ✓ → ใส่ชื่อ Lambda → Save → OK

### ขั้นตอนที่ 7: Deploy API

**1.** คลิก **Actions** → **Deploy API**

**2.** ตั้งค่า:
   - Deployment stage: **[New Stage]**
   - Stage name: `prod`

**3.** คลิก **Deploy**

**4.** ✅ **บันทึก Invoke URL** ที่ได้ เช่น:
   `https://abc12345.execute-api.ap-southeast-1.amazonaws.com/prod`

### ขั้นตอนที่ 8: ทดสอบ API ผ่าน Browser และ curl

แทนที่ `YOUR_API_URL` ด้วย URL ที่ได้จากขั้นตอนที่ 7:

```bash
# กำหนด URL (เปลี่ยนเป็น URL จริงของคุณ)
API_URL="https://abc12345.execute-api.ap-southeast-1.amazonaws.com/prod"

# ทดสอบ 1: ดึงนักศึกษาทั้งหมด
curl $API_URL/students

# ทดสอบ 2: ดึงนักศึกษา ID 1
curl $API_URL/students/1

# ทดสอบ 3: กรองตาม faculty
curl "$API_URL/students?faculty=ICT"

# ทดสอบ 4: เพิ่มนักศึกษาใหม่
curl -X POST $API_URL/students \
  -H "Content-Type: application/json" \
  -d '{"student_id":"6401005","name":"ทดสอบ API","faculty":"ICT","major":"Cloud","gpa":3.6}'

# ทดสอบ 5: แก้ไขนักศึกษา ID 1
curl -X PUT $API_URL/students/1 \
  -H "Content-Type: application/json" \
  -d '{"name":"สมชาย ใจดีมาก","gpa":3.9}'

# ทดสอบ 6: ลบนักศึกษา (ใช้ ID ของนักศึกษาที่เพิ่งสร้าง ทดสอบ 4)
curl -X DELETE $API_URL/students/5
```

> 💡 **ทดสอบง่ายๆ ผ่าน Browser**: วางลิงก์ `https://...amazonaws.com/prod/students` ในช่อง URL ของ browser เลย — ควรเห็น JSON รายชื่อนักศึกษา

---

## 📝 แบบฝึกหัด Week 3

### แบบฝึกหัดที่ 1: เพิ่ม Lambda Function ค้นหานักศึกษา

สร้าง Lambda Function ชื่อ `ict24267-search-students` โดยใช้ template นี้ (วาง code แล้วเติมในส่วน TODO):

```python
import json
import pymysql
import os

def get_db_connection():
    return pymysql.connect(
        host=os.environ['DB_HOST'],
        port=int(os.environ.get('DB_PORT', 3306)),
        database=os.environ['DB_NAME'],
        user=os.environ['DB_USER'],
        password=os.environ['DB_PASSWORD'],
        charset='utf8mb4',
        cursorclass=pymysql.cursors.DictCursor
    )

def lambda_handler(event, context):
    query_params = event.get('queryStringParameters') or {}
    keyword = query_params.get('keyword', '')

    if not keyword:
        return {"statusCode": 400,
                "body": json.dumps({"status": "error", "message": "กรุณาระบุ keyword"})}

    conn = None
    try:
        conn = get_db_connection()
        with conn.cursor() as cursor:
            # TODO: เติม SQL ที่ใช้ LIKE เพื่อค้นหาจากทั้ง name และ student_id
            #힌트: WHERE name LIKE %s OR student_id LIKE %s
            # TODO: return ผลลัพธ์ในรูปแบบ {"status": "success", "data": [...]}
            pass
    finally:
        if conn:
            conn.close()
```

### แบบฝึกหัดที่ 2: ตั้งค่า Throttling บน API Gateway

1. API Gateway → `ict24267-student-api` → **Stages** → `prod`
2. แท็บ **Default Route Settings**
3. ตั้ง **Throttling Rate**: `100` และ **Burst**: `200`
4. คลิก **Save Changes**
5. ตอบคำถาม: Throttling ช่วยป้องกันอะไร?

### คำถามท้ายบท Week 3

1. **Cold Start**: Lambda Cold Start คืออะไร? มีผลกระทบอย่างไรต่อ User Experience? และมีวิธีแก้ไขอย่างไรบ้าง?

2. **Lambda vs EC2**: เปรียบเทียบการ deploy Student Record System บน EC2 (Week 1-2) กับ Serverless Lambda (Week 3) ในแง่ของ Cost, Scalability, และ Maintenance

3. **VPC Lambda**: ทำไม Lambda ที่ต้องการเข้าถึง RDS ถึงต้องอยู่ใน VPC เดียวกัน? และการเพิ่ม VPC ส่งผลต่อ Cold Start อย่างไร?

4. **API Gateway**: อธิบายความแตกต่างระหว่าง REST API และ HTTP API ใน API Gateway พร้อมระบุว่าควรเลือกใช้แบบไหนในสถานการณ์ใด

5. **Idempotency**: ในการออกแบบ API ที่ดี ทำไม POST /students ควรมีการตรวจสอบ Idempotency? และจะ implement ได้อย่างไร?

---

---

# 📅 WEEK 4: Integration, Security & Monitoring

## วัตถุประสงค์การเรียนรู้
- รวมทุกส่วน (EC2 + RDS + Lambda + API Gateway) เข้าด้วยกัน
- ตั้งค่า Security ระดับ Production
- Monitor ระบบด้วย CloudWatch
- สร้าง Simple Frontend เพื่อใช้งาน API

## ระยะเวลา: 3 ชั่วโมง

> 💡 **Week 4 ภาพรวม**: สัปดาห์นี้ไม่ต้องเขียน code ใหม่มาก แต่จะเน้น **เพิ่มความปลอดภัย + ติดตั้ง Monitoring + สร้าง Frontend** ให้ระบบพร้อมใช้งานจริง

---

## 🔧 LAB 4-1: เก็บ Password อย่างปลอดภัยด้วย SSM Parameter Store

ใน Week 3 เราเก็บ DB Password ไว้ใน Environment Variables ซึ่งยังไม่ปลอดภัยพอ
Week 4 เราจะย้าย Password ไปเก็บใน **SSM Parameter Store** ซึ่ง encrypted และ audit ได้

> ✅ **SSM Parameter Store ฟรี** (Standard tier) — ไม่มีค่าใช้จ่าย

### ขั้นตอนที่ 1: ตรวจสอบ IAM Permission

> ⚠️ ถ้าทำ LAB 3-1 ครบแล้ว (เพิ่ม `AmazonSSMReadOnlyAccess` ไว้แล้ว) ข้ามไปขั้นตอนที่ 2 ได้เลย

หากยังไม่ได้เพิ่ม:
1. IAM → **Roles** → คลิก `ict24267-lambda-role`
2. **Add permissions** → **Attach policies**
3. ค้นหา `SSMReadOnly` → เลือก `AmazonSSMReadOnlyAccess` → **Add permissions**

### ขั้นตอนที่ 2: บันทึก Password ลง SSM

**วิธีที่ 1: ใช้ AWS CloudShell (ง่ายที่สุด — แนะนำ)**

**1.** AWS Console → คลิกไอคอน **CloudShell** (รูปหน้าต่าง Terminal) มุมบนขวา

**2.** รันทีละคำสั่ง (แทนที่ endpoint RDS จริงในบรรทัดแรก):

```bash
# เปลี่ยน YOUR_RDS_ENDPOINT เป็น endpoint จริงของคุณ
aws ssm put-parameter \
    --name "/ict24267/db/host" \
    --value "YOUR_RDS_ENDPOINT" \
    --type "SecureString" \
    --region ap-southeast-1

aws ssm put-parameter \
    --name "/ict24267/db/name" \
    --value "student_db" \
    --type "SecureString" \
    --region ap-southeast-1

aws ssm put-parameter \
    --name "/ict24267/db/user" \
    --value "admin" \
    --type "SecureString" \
    --region ap-southeast-1

aws ssm put-parameter \
    --name "/ict24267/db/password" \
    --value "ICT24267@2568" \
    --type "SecureString" \
    --region ap-southeast-1
```

**3.** ✅ แต่ละคำสั่งสำเร็จจะขึ้น `"Version": 1`

**วิธีที่ 2: ใช้ AWS Console (ถ้าไม่ถนัด CLI)**

1. ค้นหา **Systems Manager** → **Parameter Store** → **Create parameter**
2. สร้างทีละ parameter ตามตารางด้านล่าง เลือก Type: **SecureString**

| Name | Value |
|---|---|
| `/ict24267/db/host` | endpoint RDS ของคุณ |
| `/ict24267/db/name` | `student_db` |
| `/ict24267/db/user` | `admin` |
| `/ict24267/db/password` | `ICT24267@2568` |

### ขั้นตอนที่ 3: อัปเดต Lambda Functions ให้ดึง Password จาก SSM

ทำกับ **ทั้ง 2 Functions** (`ict24267-get-students` และ `ict24267-manage-students`):

**1.** Lambda → เปิด Function → แท็บ **Code**

**2.** **ลบ code เดิมทั้งหมด** แล้ว **วาง code ใหม่ด้านล่าง**

---

**สำหรับ `ict24267-get-students` — วาง code นี้ทั้งหมด:**

```python
import json
import pymysql
import boto3
import os
import logging

logger = logging.getLogger()
logger.setLevel(logging.INFO)

# เก็บ credentials ไว้ในหน่วยความจำ ไม่ต้องเรียก SSM ซ้ำทุกครั้ง
_db_credentials = None

def get_db_credentials():
    global _db_credentials
    if _db_credentials:
        return _db_credentials
    ssm = boto3.client('ssm', region_name=os.environ.get('AWS_REGION', 'ap-southeast-1'))
    response = ssm.get_parameters(
        Names=['/ict24267/db/host', '/ict24267/db/name',
               '/ict24267/db/user', '/ict24267/db/password'],
        WithDecryption=True
    )
    params = {p['Name'].split('/')[-1]: p['Value'] for p in response['Parameters']}
    _db_credentials = {
        'host': params['host'], 'database': params['name'],
        'user': params['user'], 'password': params['password']
    }
    return _db_credentials

def get_db_connection():
    creds = get_db_credentials()
    return pymysql.connect(
        host=creds['host'], port=3306,
        database=creds['database'], user=creds['user'],
        password=creds['password'], charset='utf8mb4',
        cursorclass=pymysql.cursors.DictCursor, connect_timeout=10
    )

def build_response(status_code, body):
    return {
        "statusCode": status_code,
        "headers": {"Content-Type": "application/json", "Access-Control-Allow-Origin": "*"},
        "body": json.dumps(body, ensure_ascii=False, default=str)
    }

def lambda_handler(event, context):
    logger.info(f"Event: {json.dumps(event)}")
    path_params  = event.get('pathParameters') or {}
    query_params = event.get('queryStringParameters') or {}
    student_id   = path_params.get('id')
    faculty      = query_params.get('faculty')
    min_gpa      = query_params.get('min_gpa')

    conn = None
    try:
        conn = get_db_connection()
        with conn.cursor() as cursor:
            if student_id:
                cursor.execute("SELECT * FROM students WHERE id = %s", (student_id,))
                student = cursor.fetchone()
                if not student:
                    return build_response(404, {"status": "error", "message": f"ไม่พบนักศึกษา ID {student_id}"})
                student['gpa'] = float(student['gpa']) if student['gpa'] else 0.0
                return build_response(200, {"status": "success", "data": student})
            else:
                query  = "SELECT * FROM students WHERE 1=1"
                params = []
                if faculty:
                    query += " AND faculty = %s"
                    params.append(faculty)
                if min_gpa:
                    query += " AND gpa >= %s"
                    params.append(float(min_gpa))
                query += " ORDER BY student_id"
                cursor.execute(query, params)
                students = cursor.fetchall()
                for s in students:
                    s['gpa'] = float(s['gpa']) if s['gpa'] else 0.0
                return build_response(200, {"status": "success", "count": len(students), "data": students})
    except Exception as e:
        logger.error(f"Error: {str(e)}")
        return build_response(500, {"status": "error", "message": str(e)})
    finally:
        if conn:
            conn.close()
```

---

**สำหรับ `ict24267-manage-students` — วาง code นี้ทั้งหมด:**

```python
import json
import pymysql
import boto3
import os
import logging
from datetime import datetime

logger = logging.getLogger()
logger.setLevel(logging.INFO)

_db_credentials = None

def get_db_credentials():
    global _db_credentials
    if _db_credentials:
        return _db_credentials
    ssm = boto3.client('ssm', region_name=os.environ.get('AWS_REGION', 'ap-southeast-1'))
    response = ssm.get_parameters(
        Names=['/ict24267/db/host', '/ict24267/db/name',
               '/ict24267/db/user', '/ict24267/db/password'],
        WithDecryption=True
    )
    params = {p['Name'].split('/')[-1]: p['Value'] for p in response['Parameters']}
    _db_credentials = {
        'host': params['host'], 'database': params['name'],
        'user': params['user'], 'password': params['password']
    }
    return _db_credentials

def get_db_connection():
    creds = get_db_credentials()
    return pymysql.connect(
        host=creds['host'], port=3306,
        database=creds['database'], user=creds['user'],
        password=creds['password'], charset='utf8mb4',
        cursorclass=pymysql.cursors.DictCursor, connect_timeout=10
    )

def build_response(status_code, body):
    return {
        "statusCode": status_code,
        "headers": {"Content-Type": "application/json", "Access-Control-Allow-Origin": "*"},
        "body": json.dumps(body, ensure_ascii=False, default=str)
    }

def lambda_handler(event, context):
    logger.info(f"Event: {json.dumps(event)}")
    http_method = event.get('httpMethod', '')
    path_params = event.get('pathParameters') or {}
    student_id  = path_params.get('id')
    body = {}
    if event.get('body'):
        body = json.loads(event['body'])

    conn = None
    try:
        conn = get_db_connection()
        if http_method == 'POST':
            return create_student(conn, body)
        elif http_method == 'PUT' and student_id:
            return update_student(conn, student_id, body)
        elif http_method == 'DELETE' and student_id:
            return delete_student(conn, student_id)
        else:
            return build_response(400, {"status": "error", "message": "คำขอไม่ถูกต้อง"})
    except Exception as e:
        logger.error(f"Error: {str(e)}")
        return build_response(500, {"status": "error", "message": str(e)})
    finally:
        if conn:
            conn.close()

def create_student(conn, data):
    for field in ['student_id', 'name']:
        if not data.get(field):
            return build_response(400, {"status": "error", "message": f"กรุณากรอก {field}"})
    current_thai_year = datetime.now().year + 543
    with conn.cursor() as cursor:
        cursor.execute(
            """INSERT INTO students (student_id, name, email, faculty, major, gpa, enrollment_year)
               VALUES (%s, %s, %s, %s, %s, %s, %s)""",
            (data['student_id'], data['name'], data.get('email', ''),
             data.get('faculty', ''), data.get('major', ''),
             data.get('gpa', 0.00), data.get('enrollment_year', current_thai_year))
        )
        conn.commit()
        new_id = cursor.lastrowid
        cursor.execute("SELECT * FROM students WHERE id = %s", (new_id,))
        student = cursor.fetchone()
        student['gpa'] = float(student['gpa']) if student['gpa'] else 0.0
    return build_response(201, {"status": "success", "data": student})

def update_student(conn, student_id, data):
    with conn.cursor() as cursor:
        cursor.execute("SELECT id FROM students WHERE id = %s", (student_id,))
        if not cursor.fetchone():
            return build_response(404, {"status": "error", "message": "ไม่พบนักศึกษา"})
        cursor.execute(
            """UPDATE students SET name=%s, email=%s, faculty=%s, major=%s, gpa=%s
               WHERE id=%s""",
            (data.get('name'), data.get('email'), data.get('faculty'),
             data.get('major'), data.get('gpa'), student_id)
        )
        conn.commit()
        cursor.execute("SELECT * FROM students WHERE id = %s", (student_id,))
        student = cursor.fetchone()
        student['gpa'] = float(student['gpa']) if student['gpa'] else 0.0
    return build_response(200, {"status": "success", "data": student})

def delete_student(conn, student_id):
    with conn.cursor() as cursor:
        affected = cursor.execute("DELETE FROM students WHERE id = %s", (student_id,))
        conn.commit()
    if affected == 0:
        return build_response(404, {"status": "error", "message": "ไม่พบนักศึกษา"})
    return build_response(200, {"status": "success", "message": f"ลบนักศึกษา ID {student_id} แล้ว"})
```

**4.** คลิก **Deploy** ทั้งสอง Function

**5.** ✅ ตอนนี้สามารถ **ลบ Environment Variables** `DB_PASSWORD` และ `DB_HOST` ออกจาก Lambda ได้แล้ว (ไม่จำเป็นอีกต่อไป) — แต่ยังเก็บ `DB_PORT` ไว้ได้

### ขั้นตอนที่ 4: ทดสอบว่าดึง Password จาก SSM ได้จริง

**1.** เปิด Function `ict24267-get-students` → แท็บ **Test**

**2.** รัน test เดิม (`test-get-all`) อีกครั้ง

**3.** ✅ ถ้าเห็น `"status": "success"` แสดงว่าดึง credentials จาก SSM ได้แล้ว

---

## 🔧 LAB 4-2: CloudWatch Dashboard และ Alarms

### ขั้นตอนที่ 1: สร้าง Dashboard

**1.** AWS Console → ค้นหา **CloudWatch** → เมนูซ้าย **Dashboards** → **Create dashboard**

**2.** Dashboard name: `ICT24267-Student-System` → **Create dashboard**

**3.** เพิ่ม Widget ทีละอัน โดยคลิก **Add widget** แต่ละครั้ง:

**Widget 1 — EC2 CPU:**
- เลือก **Line** → **Next**
- Metrics → **EC2** → **Per-Instance Metrics** → หา `CPUUtilization` ของ `ict24267-webserver` → ติ๊ก → **Create widget**

**Widget 2 — Lambda Invocations:**
- **Add widget** → **Line** → **Next**
- Metrics → **Lambda** → **By Function Name** → ติ๊ก `Invocations` และ `Errors` ของ `ict24267-get-students` และ `ict24267-manage-students` → **Create widget**

**Widget 3 — API Gateway:**
- **Add widget** → **Number** → **Next**
- Metrics → **API Gateway** → **By Stage** → ติ๊ก `Count`, `4XXError`, `5XXError` → **Create widget**

**Widget 4 — RDS Connections:**
- **Add widget** → **Line** → **Next**
- Metrics → **RDS** → **Per-Database Metrics** → `DatabaseConnections` ของ `ict24267-db` → **Create widget**

**4.** คลิก **Save dashboard**

### ขั้นตอนที่ 2: สร้าง Alarm แจ้งเตือนเมื่อ CPU สูง

**1.** CloudWatch → เมนูซ้าย **Alarms** → **Create alarm**

**2.** คลิก **Select metric** → **EC2** → **Per-Instance Metrics** → เลือก `CPUUtilization` ของ `ict24267-webserver` → **Select metric**

**3.** ตั้งค่า Condition:
   - Threshold type: **Static**
   - Whenever CPUUtilization is: **Greater than**
   - than: `80`

**4.** คลิก **Next** → ส่วน Notification:
   - Alarm state trigger: **In alarm**
   - Send notification to: **Create new topic**
   - Topic name: `ict24267-alerts`
   - Email endpoint: **ใส่ Email ของคุณ**
   - คลิก **Create topic**

**5.** คลิก **Next** → Alarm name: `ict24267-high-cpu` → **Create alarm**

**6.** ✅ ไปเช็ค Email แล้วคลิก **Confirm subscription** (AWS จะส่ง email มาให้ยืนยัน)

### ขั้นตอนที่ 3: สร้าง Alarm แจ้งเตือนเมื่อ Lambda Error

**1.** CloudWatch → **Create alarm** → **Select metric**

**2.** **Lambda** → **By Function Name** → `ict24267-get-students` → `Errors` → **Select metric**

**3.** Condition: **Greater than or equal** → `5`

**4.** Notification: เลือก SNS topic `ict24267-alerts` ที่สร้างไว้แล้ว

**5.** Alarm name: `ict24267-lambda-errors` → **Create alarm**

---

## 🔧 LAB 4-3: สร้าง Frontend HTML

Frontend คือหน้าเว็บที่นักศึกษาจะใช้จัดการข้อมูลแทนการพิมพ์ curl

### ขั้นตอนที่ 1: สร้างไฟล์ HTML บน EC2

SSH เข้า EC2 แล้วรันคำสั่งนี้ **ทั้งหมดในครั้งเดียว** (copy ทั้ง block):

```bash
sudo mkdir -p /var/www/html
sudo tee /var/www/html/index.html << 'HTMLEOF'
<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ICT24267 - Student Record System</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: 'Segoe UI', sans-serif; background: #f0f2f5; }
        .header {
            background: linear-gradient(135deg, #232f3e, #ff9900);
            color: white; padding: 20px 40px;
        }
        .header h1 { font-size: 1.5em; }
        .header p { font-size: 0.9em; opacity: 0.8; }
        .container { max-width: 1200px; margin: 20px auto; padding: 0 20px; }
        .card {
            background: white; border-radius: 12px;
            padding: 24px; margin-bottom: 20px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
        }
        .card h2 { color: #232f3e; margin-bottom: 16px; border-bottom: 2px solid #ff9900; padding-bottom: 8px; }
        .form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-bottom: 12px; }
        .form-group { display: flex; flex-direction: column; gap: 4px; }
        label { font-size: 0.85em; font-weight: 600; color: #555; }
        input { padding: 8px 12px; border: 1px solid #ddd; border-radius: 6px; font-size: 0.9em; }
        .btn { padding: 10px 20px; border: none; border-radius: 6px; cursor: pointer; font-weight: 600; }
        .btn-primary { background: #ff9900; color: white; }
        .btn-danger { background: #dc3545; color: white; }
        .btn:hover { opacity: 0.85; }
        table { width: 100%; border-collapse: collapse; }
        th, td { padding: 12px; text-align: left; border-bottom: 1px solid #eee; font-size: 0.9em; }
        th { background: #f8f9fa; font-weight: 700; }
        .api-config { background: #fff3cd; border: 1px solid #ffc107; border-radius: 8px; padding: 12px; margin-bottom: 16px; }
        .stats-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 16px; }
        .stat-card { background: #f8f9fa; border-radius: 8px; padding: 16px; text-align: center; }
        .stat-number { font-size: 2em; font-weight: 700; color: #ff9900; }
        #message { padding: 10px; border-radius: 6px; margin: 10px 0; display: none; }
        .success { background: #d4edda; color: #155724; }
        .error { background: #f8d7da; color: #721c24; }
        .badge { padding: 2px 8px; border-radius: 12px; font-size: 0.8em; font-weight: 600; }
        .badge-high { background: #d4edda; color: #155724; }
        .badge-mid { background: #fff3cd; color: #856404; }
        .badge-low { background: #f8d7da; color: #721c24; }
    </style>
</head>
<body>
    <div class="header">
        <h1>🎓 Student Record System</h1>
        <p>ICT 24267 Cloud Computing | ภาคการศึกษา 2/2568 | อ.อำนาจ คงเจริญถิ่น</p>
    </div>

    <div class="container">
        <div class="api-config">
            ⚙️ <strong>API URL:</strong>
            <input type="text" id="apiUrl" style="width:420px; margin-left:10px;"
                   placeholder="https://xxxxxxxxxx.execute-api.ap-southeast-1.amazonaws.com/prod">
            <button class="btn btn-primary" onclick="loadStudents()" style="margin-left:8px;">โหลดข้อมูล</button>
        </div>

        <div class="card">
            <h2>📊 สถิติภาพรวม</h2>
            <div class="stats-grid">
                <div class="stat-card"><div class="stat-number" id="totalStudents">-</div><div>นักศึกษาทั้งหมด</div></div>
                <div class="stat-card"><div class="stat-number" id="avgGpa">-</div><div>GPA เฉลี่ย</div></div>
                <div class="stat-card"><div class="stat-number" id="topGpa">-</div><div>GPA สูงสุด</div></div>
            </div>
        </div>

        <div class="card">
            <h2>➕ เพิ่มนักศึกษาใหม่</h2>
            <div id="message"></div>
            <div class="form-row">
                <div class="form-group"><label>รหัสนักศึกษา *</label><input type="text" id="newStudentId" placeholder="6401006"></div>
                <div class="form-group"><label>ชื่อ-นามสกุล *</label><input type="text" id="newName" placeholder="ชื่อภาษาไทย"></div>
                <div class="form-group"><label>Email</label><input type="email" id="newEmail" placeholder="student@example.com"></div>
                <div class="form-group"><label>คณะ</label><input type="text" id="newFaculty" value="ICT"></div>
                <div class="form-group"><label>สาขา</label><input type="text" id="newMajor" placeholder="Computer Science"></div>
                <div class="form-group"><label>GPA</label><input type="number" id="newGpa" min="0" max="4" step="0.01" placeholder="3.50"></div>
            </div>
            <button class="btn btn-primary" onclick="addStudent()">เพิ่มนักศึกษา</button>
        </div>

        <div class="card">
            <h2>📋 รายชื่อนักศึกษา</h2>
            <table>
                <thead><tr><th>รหัส</th><th>ชื่อ-นามสกุล</th><th>สาขา</th><th>GPA</th><th>จัดการ</th></tr></thead>
                <tbody id="studentsBody"><tr><td colspan="5" style="text-align:center">กรุณาตั้งค่า API URL แล้วกด "โหลดข้อมูล"</td></tr></tbody>
            </table>
        </div>
    </div>

    <script>
        const API = () => document.getElementById('apiUrl').value.replace(/\/$/, '');

        function showMsg(msg, type) {
            const el = document.getElementById('message');
            el.textContent = msg; el.className = type; el.style.display = 'block';
            setTimeout(() => el.style.display = 'none', 3000);
        }

        function gpaBadge(gpa) {
            const cls = gpa >= 3.5 ? 'badge-high' : gpa >= 2.5 ? 'badge-mid' : 'badge-low';
            return `<span class="badge ${cls}">${gpa}</span>`;
        }

        async function loadStudents() {
            try {
                const res  = await fetch(`${API()}/students`);
                const data = await res.json();
                const list = data.data || [];
                document.getElementById('totalStudents').textContent = list.length;
                if (list.length > 0) {
                    document.getElementById('avgGpa').textContent = (list.reduce((s,x) => s+x.gpa,0)/list.length).toFixed(2);
                    document.getElementById('topGpa').textContent = Math.max(...list.map(s=>s.gpa)).toFixed(2);
                }
                document.getElementById('studentsBody').innerHTML = list.map(s => `
                    <tr>
                        <td>${s.student_id}</td><td>${s.name}</td>
                        <td>${s.major || s.faculty || '-'}</td>
                        <td>${gpaBadge(s.gpa)}</td>
                        <td><button class="btn btn-danger" style="padding:4px 10px;font-size:0.8em"
                            onclick="deleteStudent(${s.id},'${s.name}')">ลบ</button></td>
                    </tr>`).join('');
            } catch(e) { showMsg('❌ เชื่อมต่อ API ไม่ได้: ' + e.message, 'error'); }
        }

        async function addStudent() {
            const s = {
                student_id: document.getElementById('newStudentId').value,
                name:       document.getElementById('newName').value,
                email:      document.getElementById('newEmail').value,
                faculty:    document.getElementById('newFaculty').value,
                major:      document.getElementById('newMajor').value,
                gpa:        parseFloat(document.getElementById('newGpa').value) || 0
            };
            if (!s.student_id || !s.name) { showMsg('⚠️ กรอกรหัสและชื่อให้ครบ', 'error'); return; }
            try {
                const res  = await fetch(`${API()}/students`, {method:'POST', headers:{'Content-Type':'application/json'}, body: JSON.stringify(s)});
                const data = await res.json();
                if (data.status === 'success') {
                    showMsg('✅ เพิ่มนักศึกษาสำเร็จ', 'success');
                    loadStudents();
                    ['newStudentId','newName','newEmail','newMajor','newGpa'].forEach(id => document.getElementById(id).value='');
                } else { showMsg('❌ ' + data.message, 'error'); }
            } catch(e) { showMsg('❌ ' + e.message, 'error'); }
        }

        async function deleteStudent(id, name) {
            if (!confirm(`ยืนยันการลบ "${name}"?`)) return;
            try {
                const res  = await fetch(`${API()}/students/${id}`, {method:'DELETE'});
                const data = await res.json();
                if (data.status === 'success') { showMsg('✅ ลบสำเร็จ', 'success'); loadStudents(); }
            } catch(e) { showMsg('❌ ' + e.message, 'error'); }
        }
    </script>
</body>
</html>
HTMLEOF
```

### ขั้นตอนที่ 2: ตั้งค่า Nginx ให้แสดงหน้าเว็บ

```bash
sudo tee /etc/nginx/conf.d/default.conf << 'EOF'
server {
    listen 80;
    server_name _;

    location / {
        root /var/www/html;
        index index.html;
    }

    location /api/ {
        proxy_pass http://127.0.0.1:5000/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
EOF

sudo systemctl reload nginx
```

### ขั้นตอนที่ 3: ทดสอบ Frontend

**1.** เปิด Browser แล้วไปที่ `http://YOUR_EC2_PUBLIC_IP`

**2.** ใส่ API Gateway URL ในช่อง "API URL" แล้วคลิก **โหลดข้อมูล**

**3.** ✅ ควรเห็นรายชื่อนักศึกษาแสดงในตาราง

---

## 🔧 LAB 4-4: Architecture Diagram และ Cost Estimation

### สรุป Architecture ทั้งระบบ

```
Internet
    │
    ├─── Frontend (EC2 t2.micro + Nginx)
    │         │
    │         └─── Flask API (Port 5000)
    │                   │
    │                   └─── RDS MySQL (db.t3.micro)
    │
    └─── API Gateway (REST API)
              │
              ├─── GET  /students     → Lambda: ict24267-get-students
              ├─── POST /students     → Lambda: ict24267-manage-students
              ├─── PUT  /students/{id}→ Lambda: ict24267-manage-students
              └─── DELETE /students/{id}→Lambda: ict24267-manage-students
                              │
                              └─── RDS MySQL (shared with EC2 app)

CloudWatch → Monitor EC2 + Lambda + RDS + API Gateway
SSM Parameter Store → Store DB Credentials
IAM → Roles and Policies
```

### Free Tier Cost Estimation (ต่อเดือน)

| Service | Usage | Free Tier | ค่าใช้จ่าย |
|---|---|---|---|
| EC2 t2.micro | ~720 ชม. | 750 ชม./เดือน | $0.00 ✅ |
| RDS db.t3.micro | ~720 ชม. | 750 ชม./เดือน | $0.00 ✅ |
| Lambda | ~1,000 invocations | 1,000,000/เดือน | $0.00 ✅ |
| API Gateway | ~1,000 calls | 1,000,000/เดือน | $0.00 ✅ |
| CloudWatch | Basic monitoring | Always Free | $0.00 ✅ |
| SSM Parameter Store | 4 parameters | 10,000 free | $0.00 ✅ |
| Data Transfer | < 1 GB | 1 GB/เดือน | $0.00 ✅ |
| **รวมทั้งหมด** | | | **$0.00** |

---

## 🔧 LAB 4-5: Cleanup — ป้องกันค่าใช้จ่ายหลังสิ้นสุด LAB

> ⚠️ **สำคัญ**: หลังสิ้นสุดการใช้งาน ต้องทำตามขั้นตอนนี้เพื่อหลีกเลี่ยงค่าใช้จ่าย

```
ลำดับการ Cleanup:

1. API Gateway → ลบ Stages → ลบ API
2. Lambda → ลบ Functions ทั้งหมด
3. EC2 → Stop Instance (หรือ Terminate ถ้าไม่ใช้แล้ว)
4. RDS → Stop DB Instance (หยุดชั่วคราว สูงสุด 7 วัน)
   หรือ Delete DB Instance ถ้าไม่ใช้แล้ว (ต้อง Create Final Snapshot)
5. Elastic IP → ถ้า Disassociate แล้ว ต้อง Release ด้วย
6. CloudWatch → ลบ Alarms ที่ไม่ใช้
7. SSM Parameter Store → ลบ Parameters
```

---

## 📝 แบบฝึกหัด Week 4

### แบบฝึกหัดที่ 1: เพิ่ม Authentication
เพิ่ม API Key Authentication บน API Gateway:
1. API Gateway → API Keys → Create API Key
2. Usage Plans → Create Usage Plan (1000 requests/day)
3. Associate API Key กับ Usage Plan
4. ทดสอบเรียก API พร้อม Header `x-api-key: <key>`

### แบบฝึกหัดที่ 2: CloudWatch Logs Insights
ใน CloudWatch → Logs Insights ทดลองรัน Query:
```
# ดู Lambda Errors
fields @timestamp, @message
| filter @message like /ERROR/
| sort @timestamp desc
| limit 20

# ดู Response Time ของ Lambda
fields @timestamp, @duration
| filter @type = "REPORT"
| stats avg(@duration), max(@duration) by bin(5m)
```

### คำถามท้ายบท Week 4

1. **Architecture Decision**: ในโปรเจกต์นี้มีทั้ง EC2+Flask และ Lambda+API Gateway ที่ทำงานคล้ายกัน ในสภาพแวดล้อม Production จริง คุณจะเลือกแนวทางใด และเพราะเหตุใด?

2. **Security Layers**: อธิบาย Defense in Depth ของระบบที่สร้างมาตลอด 4 สัปดาห์ มีกี่ Layer และแต่ละ Layer ป้องกันอะไร?

3. **Scalability**: ถ้าผู้ใช้ระบบเพิ่มจาก 10 คนเป็น 10,000 คนพร้อมกัน ส่วนไหนของระบบจะเป็น Bottleneck ก่อน และจะแก้ไขอย่างไร?

4. **Disaster Recovery**: อธิบาย RTO (Recovery Time Objective) และ RPO (Recovery Point Objective) ของระบบนี้ และทำอย่างไรให้ดีขึ้น?

5. **Cost Optimization**: นอกจาก Free Tier แล้ว ถ้าต้องเสียเงินจริง มีวิธีใดบ้างที่จะช่วยลดค่าใช้จ่าย AWS สำหรับระบบนี้?

---

# 📚 ภาคผนวก

## A. คำสั่ง AWS CLI ที่ใช้บ่อย

```bash
# ตรวจสอบ EC2 Instances
aws ec2 describe-instances --query 'Reservations[*].Instances[*].[InstanceId,State.Name,PublicIpAddress]' --output table

# ดู RDS Instances
aws rds describe-db-instances --query 'DBInstances[*].[DBInstanceIdentifier,DBInstanceStatus,Endpoint.Address]' --output table

# ดู Lambda Functions
aws lambda list-functions --query 'Functions[*].[FunctionName,Runtime,LastModified]' --output table

# ดู API Gateway
aws apigateway get-rest-apis --query 'items[*].[id,name]' --output table

# ตรวจสอบค่าใช้จ่ายปัจจุบัน
aws ce get-cost-and-usage \
    --time-period Start=$(date -d '1 month ago' +%Y-%m-01),End=$(date +%Y-%m-%d) \
    --granularity MONTHLY \
    --metrics BlendedCost \
    --output table
```

## B. สรุป Free Tier Checklist
 
```
ก่อนเริ่ม LAB ทุกครั้ง:
[ ] ตรวจสอบ AWS Billing Dashboard
[ ] มี Budget Alert ตั้งค่าไว้แล้ว
[ ] ใช้ ap-southeast-1 หรือ us-east-1 เท่านั้น
 
ระหว่าง LAB:
[ ] EC2: ใช้ t2.micro หรือ t3.micro เท่านั้น
[ ] RDS: ใช้ db.t3.micro, Single-AZ, 20GB เท่านั้น
[ ] ไม่สร้าง NAT Gateway (มีค่าใช้จ่าย!)
[ ] ไม่ใช้ Application/Network Load Balancer (มีค่าใช้จ่าย!)
 
หลัง LAB ทุกครั้ง:
[ ] Stop หรือ Terminate EC2 Instances
[ ] Stop หรือ Delete RDS Instances
[ ] Release Elastic IPs ที่ไม่ใช้
[ ] ลบ Lambda Functions ที่ไม่จำเป็น
[ ] ลบ API Gateway Stages ที่ไม่ใช้
[ ] ตรวจสอบ Billing ซ้ำ
```
 
## C. Resources เพิ่มเติม
 
| แหล่งเรียนรู้ | URL |
|---|---|
| AWS Free Tier Details | https://aws.amazon.com/free/ |
| AWS Documentation | https://docs.aws.amazon.com/ |
| AWS Lambda Developer Guide | https://docs.aws.amazon.com/lambda/latest/dg/ |
| AWS RDS User Guide | https://docs.aws.amazon.com/rds/ |
| AWS API Gateway Guide | https://docs.aws.amazon.com/apigateway/ |
| AWS Well-Architected Framework | https://aws.amazon.com/architecture/well-architected/ |
| AWS Skill Builder (Free Courses) | https://skillbuilder.aws/ |
| AWS Training & Certification | https://aws.amazon.com/training/ |
 
---
 
*คู่มือ LAB นี้จัดทำสำหรับ**วิชา ICT 24267 Cloud Computing** ภาคการศึกษา 2/2568*  
*ผู้สอน: อาจารย์อำนาจ คงเจริญถิ่น*  
*เนื้อหาอัปเดตตาม AWS Free Tier 2026*
