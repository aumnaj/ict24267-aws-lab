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
| **EC2** | t2.micro หรือ t3.micro, 750 ชม./เดือน | 12 เดือนแรก |
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
- ✅ ใช้ **t2.micro** หรือ **t3.micro** เท่านั้น
- ✅ **Amazon Linux 2023** หรือ **Ubuntu 22.04 LTS** (Free Tier eligible)
- ✅ Storage: **8 GB gp2/gp3** (ไม่เกิน 30 GB รวม)
- ❌ **อย่า** สร้าง Instance หลายตัวพร้อมกัน (750 ชม./เดือน รวมทุก Instance)

### ขั้นตอนที่ 1: สร้าง Key Pair
1. AWS Console → **EC2** → **Key Pairs** → **Create key pair**
2. Name: `ict24267-key`
3. Key pair type: **RSA**
4. Private key file format: **.pem** (macOS/Linux) หรือ **.ppk** (Windows + PuTTY)
5. คลิก **Create key pair** → บันทึกไฟล์ไว้ในที่ปลอดภัย

```bash
# macOS/Linux: ปรับ permission ของ key file
chmod 400 ~/Downloads/ict24267-key.pem
```

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
4. Instance type: **t2.micro** ✅
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

### ขั้นตอนที่ 4: เชื่อมต่อผ่าน SSH
```bash
# เชื่อมต่อ EC2 Instance
ssh -i ~/Downloads/ict24267-key.pem ec2-user@<YOUR_PUBLIC_IP>

# ตรวจสอบสถานะ app
sudo systemctl status student-app

# ดู log
sudo journalctl -u student-app -f

# ตรวจสอบ User Data log
cat /var/log/user-data.log
```

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
Master password:        ICT24267@2568  (หรือกำหนดเอง)

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
sudo yum install -y mysql

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
DB_PASSWORD=ICT24267@2568
SECRET_KEY=ict24267-secret-key-2568
EOF

chmod 600 /home/ec2-user/student-app/.env
```

### สร้างไฟล์ `database.py`
```python
# /home/ec2-user/student-app/database.py
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
        cursorclass=pymysql.cursors.DictCursor,
        autocommit=True
    )

def execute_query(query, params=None, fetch=True):
    """Helper function สำหรับรัน Query"""
    conn = get_connection()
    try:
        with conn.cursor() as cursor:
            cursor.execute(query, params or ())
            if fetch:
                return cursor.fetchall()
            return cursor.lastrowid
    finally:
        conn.close()
```

### อัปเดตไฟล์ `app.py` หลัก
```python
# /home/ec2-user/student-app/app.py (Week 2 Version)
from flask import Flask, jsonify, request
from datetime import datetime
import os
from dotenv import load_dotenv
from database import execute_query, get_connection

load_dotenv()

app = Flask(__name__)

# ============================================================
# ROOT & HEALTH ENDPOINTS
# ============================================================

@app.route('/')
def index():
    return jsonify({
        "message": "🎓 Student Record System - Week 2 (with RDS)",
        "course": "ICT 24267 Cloud Computing",
        "semester": "2/2568",
        "server_time": datetime.now().strftime("%Y-%m-%d %H:%M:%S"),
        "version": "2.0.0",
        "database": "MySQL RDS"
    })

@app.route('/health')
def health():
    """Health check รวมถึง Database connectivity"""
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

# ============================================================
# STUDENTS CRUD ENDPOINTS
# ============================================================

@app.route('/students', methods=['GET'])
def get_students():
    """ดึงข้อมูลนักศึกษาทั้งหมด"""
    try:
        # รองรับ query parameters
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
        return jsonify({
            "status": "success",
            "count": len(students),
            "data": students
        })
    except Exception as e:
        return jsonify({"status": "error", "message": str(e)}), 500

@app.route('/students/<int:student_id>', methods=['GET'])
def get_student(student_id):
    """ดึงข้อมูลนักศึกษาตาม ID"""
    try:
        result = execute_query(
            "SELECT * FROM students WHERE id = %s", 
            (student_id,)
        )
        if result:
            return jsonify({"status": "success", "data": result[0]})
        return jsonify({"status": "error", "message": "Student not found"}), 404
    except Exception as e:
        return jsonify({"status": "error", "message": str(e)}), 500

@app.route('/students', methods=['POST'])
def create_student():
    """เพิ่มนักศึกษาใหม่"""
    try:
        data = request.get_json()
        required_fields = ['student_id', 'name']
        
        for field in required_fields:
            if not data.get(field):
                return jsonify({
                    "status": "error", 
                    "message": f"Missing required field: {field}"
                }), 400
        
        new_id = execute_query(
            """INSERT INTO students 
               (student_id, name, email, faculty, major, gpa, enrollment_year)
               VALUES (%s, %s, %s, %s, %s, %s, %s)""",
            (
                data['student_id'], data['name'],
                data.get('email', ''), data.get('faculty', ''),
                data.get('major', ''), data.get('gpa', 0.00),
                data.get('enrollment_year', datetime.now().year + 543)
            ),
            fetch=False
        )
        
        student = execute_query(
            "SELECT * FROM students WHERE id = %s", (new_id,)
        )
        return jsonify({"status": "success", "data": student[0]}), 201
        
    except Exception as e:
        return jsonify({"status": "error", "message": str(e)}), 500

@app.route('/students/<int:student_id>', methods=['PUT'])
def update_student(student_id):
    """อัปเดตข้อมูลนักศึกษา"""
    try:
        data = request.get_json()
        
        execute_query(
            """UPDATE students 
               SET name=%s, email=%s, faculty=%s, major=%s, gpa=%s
               WHERE id=%s""",
            (
                data.get('name'), data.get('email'),
                data.get('faculty'), data.get('major'),
                data.get('gpa'), student_id
            ),
            fetch=False
        )
        
        student = execute_query(
            "SELECT * FROM students WHERE id = %s", (student_id,)
        )
        if student:
            return jsonify({"status": "success", "data": student[0]})
        return jsonify({"status": "error", "message": "Student not found"}), 404
        
    except Exception as e:
        return jsonify({"status": "error", "message": str(e)}), 500

@app.route('/students/<int:student_id>', methods=['DELETE'])
def delete_student(student_id):
    """ลบข้อมูลนักศึกษา"""
    try:
        execute_query(
            "DELETE FROM students WHERE id = %s", 
            (student_id,), 
            fetch=False
        )
        return jsonify({
            "status": "success", 
            "message": f"Student ID {student_id} deleted"
        })
    except Exception as e:
        return jsonify({"status": "error", "message": str(e)}), 500

# ============================================================
# COURSES ENDPOINTS
# ============================================================

@app.route('/courses', methods=['GET'])
def get_courses():
    courses = execute_query("SELECT * FROM courses ORDER BY course_code")
    return jsonify({"status": "success", "count": len(courses), "data": courses})

@app.route('/courses', methods=['POST'])
def create_course():
    data = request.get_json()
    new_id = execute_query(
        "INSERT INTO courses (course_code, course_name, credits, instructor) VALUES (%s, %s, %s, %s)",
        (data['course_code'], data['course_name'], data.get('credits', 3), data.get('instructor', '')),
        fetch=False
    )
    course = execute_query("SELECT * FROM courses WHERE id = %s", (new_id,))
    return jsonify({"status": "success", "data": course[0]}), 201

# ============================================================
# STATISTICS ENDPOINT
# ============================================================

@app.route('/stats')
def get_stats():
    """สถิติภาพรวม"""
    total_students = execute_query("SELECT COUNT(*) as count FROM students")[0]['count']
    avg_gpa = execute_query("SELECT AVG(gpa) as avg FROM students")[0]['avg']
    top_students = execute_query(
        "SELECT name, student_id, gpa FROM students ORDER BY gpa DESC LIMIT 3"
    )
    
    return jsonify({
        "status": "success",
        "data": {
            "total_students": total_students,
            "average_gpa": round(float(avg_gpa or 0), 2),
            "top_students": top_students
        }
    })

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000, debug=False)
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

---

## 🔧 LAB 3-1: สร้าง IAM Role สำหรับ Lambda

### ขั้นตอนที่ 1: สร้าง IAM Role
1. AWS Console → **IAM** → **Roles** → **Create role**
2. Trusted entity: **AWS service** → **Lambda**
3. เพิ่ม Permissions policies:
   - `AWSLambdaVPCAccessExecutionRole` (สำหรับเข้าถึง VPC/RDS)
   - `AWSLambdaBasicExecutionRole` (สำหรับ CloudWatch Logs)
4. Role name: `ict24267-lambda-role`

---

## 🔧 LAB 3-2: สร้าง Lambda Layer สำหรับ PyMySQL

เนื่องจาก Lambda ไม่มี `pymysql` ติดตั้งมาให้ ต้องสร้าง Layer:

```bash
# รันบนเครื่อง Local หรือ EC2
mkdir -p lambda-layer/python
pip3 install pymysql -t lambda-layer/python/
cd lambda-layer
zip -r pymysql-layer.zip python/
```

1. AWS Console → **Lambda** → **Layers** → **Create layer**
2. Name: `pymysql-layer`
3. Upload: `pymysql-layer.zip`
4. Compatible runtimes: **Python 3.11**
5. คลิก **Create**

---

## 🔧 LAB 3-3: สร้าง Lambda Functions

### Function 1: `ict24267-get-students`

1. Lambda → **Create function**
2. Function name: `ict24267-get-students`
3. Runtime: **Python 3.11**
4. Execution role: **Use an existing role** → `ict24267-lambda-role`

**โค้ด Lambda Function:**
```python
# lambda_get_students.py
import json
import pymysql
import os
import logging

logger = logging.getLogger()
logger.setLevel(logging.INFO)

def get_db_connection():
    """สร้าง RDS Connection"""
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

def lambda_handler(event, context):
    """
    Lambda Handler สำหรับดึงข้อมูลนักศึกษา
    Supports: GET /students และ GET /students/{id}
    """
    logger.info(f"Event: {json.dumps(event)}")
    
    # ดึง path parameters
    path_params = event.get('pathParameters') or {}
    student_id = path_params.get('id')
    
    # ดึง query string parameters
    query_params = event.get('queryStringParameters') or {}
    faculty = query_params.get('faculty')
    min_gpa = query_params.get('min_gpa')
    
    conn = None
    try:
        conn = get_db_connection()
        
        with conn.cursor() as cursor:
            if student_id:
                # ดึงนักศึกษาคนเดียว
                cursor.execute(
                    "SELECT * FROM students WHERE id = %s", 
                    (student_id,)
                )
                student = cursor.fetchone()
                
                if not student:
                    return build_response(404, {
                        "status": "error",
                        "message": f"Student ID {student_id} not found"
                    })
                
                # แปลง Decimal เป็น float
                student['gpa'] = float(student['gpa']) if student['gpa'] else 0.0
                
                return build_response(200, {
                    "status": "success",
                    "data": student
                })
            else:
                # ดึงนักศึกษาทั้งหมด พร้อม filters
                query = "SELECT * FROM students WHERE 1=1"
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
                
                # แปลง Decimal เป็น float
                for s in students:
                    s['gpa'] = float(s['gpa']) if s['gpa'] else 0.0
                
                return build_response(200, {
                    "status": "success",
                    "count": len(students),
                    "data": students
                })
                
    except pymysql.Error as e:
        logger.error(f"Database error: {str(e)}")
        return build_response(500, {
            "status": "error",
            "message": f"Database error: {str(e)}"
        })
    except Exception as e:
        logger.error(f"Unexpected error: {str(e)}")
        return build_response(500, {
            "status": "error",
            "message": "Internal server error"
        })
    finally:
        if conn:
            conn.close()

def build_response(status_code, body):
    """สร้าง HTTP Response ที่ถูกต้องสำหรับ API Gateway"""
    return {
        "statusCode": status_code,
        "headers": {
            "Content-Type": "application/json",
            "Access-Control-Allow-Origin": "*",
            "Access-Control-Allow-Headers": "Content-Type",
            "Access-Control-Allow-Methods": "GET,POST,PUT,DELETE,OPTIONS"
        },
        "body": json.dumps(body, ensure_ascii=False, default=str)
    }
```

5. เพิ่ม **Environment Variables**:
   - `DB_HOST`: endpoint ของ RDS
   - `DB_PORT`: 3306
   - `DB_NAME`: student_db
   - `DB_USER`: admin
   - `DB_PASSWORD`: ICT24267@2568

6. เพิ่ม **VPC Configuration** (เพื่อเข้าถึง RDS):
   - VPC: Default VPC
   - Subnets: เลือกทุก subnet
   - Security groups: `ict24267-rds-sg`

7. เพิ่ม **Layer**: เลือก `pymysql-layer` ที่สร้างไว้

### Function 2: `ict24267-manage-students`

สร้าง Lambda Function อีกตัวสำหรับ POST/PUT/DELETE:

```python
# lambda_manage_students.py
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

def lambda_handler(event, context):
    logger.info(f"Event: {json.dumps(event)}")
    
    http_method = event.get('httpMethod', '')
    path_params = event.get('pathParameters') or {}
    student_id = path_params.get('id')
    
    # แปลง body
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
            return build_response(400, {"status": "error", "message": "Invalid request"})
            
    except Exception as e:
        logger.error(f"Error: {str(e)}")
        return build_response(500, {"status": "error", "message": str(e)})
    finally:
        if conn:
            conn.close()

def create_student(conn, data):
    required = ['student_id', 'name']
    for field in required:
        if not data.get(field):
            return build_response(400, {
                "status": "error",
                "message": f"Missing required field: {field}"
            })
    
    with conn.cursor() as cursor:
        cursor.execute(
            """INSERT INTO students (student_id, name, email, faculty, major, gpa, enrollment_year)
               VALUES (%s, %s, %s, %s, %s, %s, %s)""",
            (
                data['student_id'], data['name'],
                data.get('email', ''), data.get('faculty', ''),
                data.get('major', ''), data.get('gpa', 0.00),
                data.get('enrollment_year', 2567)
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
        
    if not student:
        return build_response(404, {"status": "error", "message": "Student not found"})
    
    student['gpa'] = float(student['gpa']) if student['gpa'] else 0.0
    return build_response(200, {"status": "success", "data": student})

def delete_student(conn, student_id):
    with conn.cursor() as cursor:
        affected = cursor.execute(
            "DELETE FROM students WHERE id = %s", (student_id,)
        )
        conn.commit()
    
    if affected == 0:
        return build_response(404, {"status": "error", "message": "Student not found"})
    
    return build_response(200, {
        "status": "success",
        "message": f"Student ID {student_id} deleted successfully"
    })

def build_response(status_code, body):
    return {
        "statusCode": status_code,
        "headers": {
            "Content-Type": "application/json",
            "Access-Control-Allow-Origin": "*",
            "Access-Control-Allow-Headers": "Content-Type",
            "Access-Control-Allow-Methods": "GET,POST,PUT,DELETE,OPTIONS"
        },
        "body": json.dumps(body, ensure_ascii=False, default=str)
    }
```

---

## 🔧 LAB 3-4: สร้าง API Gateway

### ขั้นตอนที่ 1: สร้าง REST API
1. AWS Console → **API Gateway** → **Create API**
2. เลือก **REST API** → **Build**
3. Protocol: **REST**
4. Create new API: **New API**
5. API name: `ict24267-student-api`
6. Endpoint Type: **Regional**
7. คลิก **Create API**

### ขั้นตอนที่ 2: สร้าง Resources และ Methods

**สร้าง `/students` resource:**
1. Actions → **Create Resource**
2. Resource Name: `students`
3. Resource Path: `students`
4. Enable API Gateway CORS: ✅
5. Create Resource

**เพิ่ม Method GET บน /students:**
1. เลือก `/students` → Actions → **Create Method** → **GET**
2. Integration type: **Lambda Function**
3. Lambda Function: `ict24267-get-students`
4. Save → OK (Allow API Gateway to invoke Lambda)

**เพิ่ม Method POST บน /students:**
1. เลือก `/students` → Actions → **Create Method** → **POST**
2. Lambda Function: `ict24267-manage-students`

**สร้าง `/students/{id}` resource:**
1. เลือก `/students` → Actions → **Create Resource**
2. Resource Name: `student`
3. Resource Path: `{id}` (ใส่ curly braces)
4. Create Resource

**เพิ่ม Methods บน /students/{id}:**
- GET → `ict24267-get-students`
- PUT → `ict24267-manage-students`
- DELETE → `ict24267-manage-students`

### ขั้นตอนที่ 3: Deploy API
1. Actions → **Deploy API**
2. Deployment stage: **[New Stage]**
3. Stage name: `prod`
4. คลิก **Deploy**
5. บันทึก **Invoke URL**: `https://xxxxxxxxxx.execute-api.ap-southeast-1.amazonaws.com/prod`

### ขั้นตอนที่ 4: ทดสอบ API
```bash
# กำหนด API Base URL
API_URL="https://xxxxxxxxxx.execute-api.ap-southeast-1.amazonaws.com/prod"

# GET ทุก students
curl $API_URL/students

# GET นักศึกษาคนเดียว
curl $API_URL/students/1

# GET ด้วย filter
curl "$API_URL/students?faculty=ICT&min_gpa=3.5"

# POST เพิ่มนักศึกษาใหม่
curl -X POST $API_URL/students \
  -H "Content-Type: application/json" \
  -d '{
    "student_id": "6401005",
    "name": "ทดสอบ ระบบ",
    "email": "test@api.com",
    "faculty": "ICT",
    "major": "Cloud Technology",
    "gpa": 3.60,
    "enrollment_year": 2564
  }'

# PUT อัปเดต
curl -X PUT $API_URL/students/1 \
  -H "Content-Type: application/json" \
  -d '{"name": "สมชาย ใจดีมาก", "gpa": 3.65}'

# DELETE ลบนักศึกษา
curl -X DELETE $API_URL/students/5
```

---

## 🔧 LAB 3-5: Lambda สำหรับงาน Scheduled (CloudWatch Events)

สร้าง Lambda Function สำหรับ **สรุปสถิติรายวัน** (ตัวอย่าง Always Free Use Case):

```python
# lambda_daily_report.py
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
    """
    Lambda ที่ถูก trigger โดย EventBridge (CloudWatch Events)
    ทำงานทุกวันเพื่อสร้างสรุปสถิติ
    """
    logger.info("Daily report Lambda triggered")
    
    conn = None
    try:
        conn = get_db_connection()
        report = generate_daily_report(conn)
        
        logger.info(f"Daily Report Generated: {json.dumps(report, ensure_ascii=False)}")
        
        return {
            "statusCode": 200,
            "body": json.dumps({
                "message": "Daily report generated successfully",
                "report": report
            }, ensure_ascii=False)
        }
    except Exception as e:
        logger.error(f"Error generating report: {str(e)}")
        raise
    finally:
        if conn:
            conn.close()

def generate_daily_report(conn):
    with conn.cursor() as cursor:
        # จำนวนนักศึกษาทั้งหมด
        cursor.execute("SELECT COUNT(*) as total FROM students")
        total = cursor.fetchone()['total']
        
        # GPA เฉลี่ย
        cursor.execute("SELECT AVG(gpa) as avg_gpa FROM students")
        avg_gpa = cursor.fetchone()['avg_gpa']
        
        # แจกแจงตาม Faculty
        cursor.execute("""
            SELECT faculty, COUNT(*) as count, AVG(gpa) as avg_gpa
            FROM students
            GROUP BY faculty
            ORDER BY count DESC
        """)
        by_faculty = cursor.fetchall()
        
        # Top 5 นักศึกษา
        cursor.execute("""
            SELECT name, student_id, gpa 
            FROM students 
            ORDER BY gpa DESC 
            LIMIT 5
        """)
        top_students = cursor.fetchall()
        
    return {
        "report_date": datetime.now().strftime("%Y-%m-%d"),
        "total_students": total,
        "average_gpa": round(float(avg_gpa or 0), 2),
        "by_faculty": [
            {
                "faculty": r['faculty'],
                "count": r['count'],
                "avg_gpa": round(float(r['avg_gpa'] or 0), 2)
            }
            for r in by_faculty
        ],
        "top_5_students": [
            {"name": s['name'], "student_id": s['student_id'], "gpa": float(s['gpa'])}
            for s in top_students
        ]
    }
```

### ตั้ง Schedule ด้วย EventBridge
1. Lambda Function → **Configuration** → **Triggers** → **Add trigger**
2. Trigger source: **EventBridge (CloudWatch Events)**
3. Rule: **Create a new rule**
4. Rule name: `ict24267-daily-report`
5. Schedule expression: `cron(0 1 * * ? *)` (ทุกวัน 01:00 UTC = 08:00 น. ไทย)
6. Add

---

## 📝 แบบฝึกหัด Week 3

### แบบฝึกหัดที่ 1: เพิ่ม Lambda Function ใหม่
สร้าง Lambda Function ชื่อ `ict24267-search-students` ที่:
- รับ query parameter `keyword`
- ค้นหาจากทั้ง `name` และ `student_id`
- Return รายการที่ตรงกัน

```python
# Template ให้เติมให้สมบูรณ์
def lambda_handler(event, context):
    query_params = event.get('queryStringParameters') or {}
    keyword = query_params.get('keyword', '')
    
    # TODO: เขียน SQL query ที่ใช้ LIKE เพื่อค้นหา
    # TODO: Return ผลลัพธ์ในรูปแบบที่ถูกต้อง
    pass
```

### แบบฝึกหัดที่ 2: API Gateway Throttling
1. ไปที่ **API Gateway → ict24267-student-api → Stages → prod**
2. เปิด **Default Method Throttling**
3. ตั้ง Rate: `100`, Burst: `200`
4. Save Changes
5. อธิบายว่า Throttling มีประโยชน์อย่างไร

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

---

## 🔧 LAB 4-1: Secrets Manager สำหรับ Database Credentials

> ⚠️ AWS Secrets Manager **ไม่ฟรี** ($0.40/secret/month) แต่มี **30 วันทดลองฟรี**  
> ทางเลือกฟรี: ใช้ **SSM Parameter Store (Standard)** ซึ่ง Free Tier รองรับ

### ใช้ SSM Parameter Store (Free)
```python
# อัปเดต Lambda Functions ให้ดึง credentials จาก SSM

import boto3
import json
import os

def get_db_credentials():
    """
    ดึง Database credentials จาก AWS SSM Parameter Store
    (ฟรี และปลอดภัยกว่าการเก็บใน Environment Variables)
    """
    ssm = boto3.client('ssm', region_name='ap-southeast-1')
    
    response = ssm.get_parameters(
        Names=[
            '/ict24267/db/host',
            '/ict24267/db/name',
            '/ict24267/db/user',
            '/ict24267/db/password'
        ],
        WithDecryption=True
    )
    
    params = {p['Name'].split('/')[-1]: p['Value'] 
              for p in response['Parameters']}
    
    return {
        'host': params['host'],
        'database': params['name'],
        'user': params['user'],
        'password': params['password']
    }
```

### สร้าง Parameters ใน SSM
```bash
# รันบน AWS CLI หรือ CloudShell
aws ssm put-parameter \
    --name "/ict24267/db/host" \
    --value "ict24267-db.xxxxxxxxxx.ap-southeast-1.rds.amazonaws.com" \
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

---

## 🔧 LAB 4-2: CloudWatch Dashboard และ Alarms

### สร้าง CloudWatch Dashboard
1. AWS Console → **CloudWatch** → **Dashboards** → **Create dashboard**
2. Name: `ICT24267-Student-System`
3. เพิ่ม Widgets:

**Widget 1: EC2 CPU Utilization**
- Add widget → Line
- Metrics → EC2 → Per-Instance Metrics
- CPUUtilization → Instance: `ict24267-webserver`

**Widget 2: Lambda Invocations**
- Add widget → Line
- Metrics → Lambda → By Function Name
- Invocations, Duration, Errors
- Function: `ict24267-get-students`, `ict24267-manage-students`

**Widget 3: API Gateway Requests**
- Add widget → Number
- Metrics → API Gateway → By Stage
- Count, 4XXError, 5XXError

**Widget 4: RDS Connections**
- Add widget → Line
- Metrics → RDS → Per-Database Metrics
- DatabaseConnections → DB: `ict24267-db`

### สร้าง CloudWatch Alarms
```
1. CloudWatch → Alarms → Create alarm

Alarm 1: EC2 High CPU
- Metric: EC2 > CPUUtilization > ict24267-webserver
- Condition: > 80% for 2 consecutive periods (5 min each)
- Action: Send notification to email (SNS)

Alarm 2: Lambda Errors
- Metric: Lambda > Errors > ict24267-get-students
- Condition: >= 5 errors in 5 minutes
- Action: Send notification to email
```

---

## 🔧 LAB 4-3: สร้าง Frontend HTML สำหรับ Student System

### สร้างไฟล์ `index.html` บน EC2
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
            display: flex; align-items: center; gap: 15px;
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
        input, select {
            padding: 8px 12px; border: 1px solid #ddd;
            border-radius: 6px; font-size: 0.9em;
        }
        .btn {
            padding: 10px 20px; border: none; border-radius: 6px;
            cursor: pointer; font-weight: 600; transition: all 0.2s;
        }
        .btn-primary { background: #ff9900; color: white; }
        .btn-danger { background: #dc3545; color: white; }
        .btn-secondary { background: #6c757d; color: white; }
        .btn:hover { opacity: 0.85; transform: translateY(-1px); }
        table { width: 100%; border-collapse: collapse; }
        th, td { padding: 12px; text-align: left; border-bottom: 1px solid #eee; font-size: 0.9em; }
        th { background: #f8f9fa; font-weight: 700; color: #333; }
        tr:hover { background: #fff8f0; }
        .badge {
            padding: 2px 8px; border-radius: 12px; font-size: 0.8em;
            font-weight: 600;
        }
        .badge-high { background: #d4edda; color: #155724; }
        .badge-mid { background: #fff3cd; color: #856404; }
        .badge-low { background: #f8d7da; color: #721c24; }
        .api-config { background: #fff3cd; border: 1px solid #ffc107; border-radius: 8px; padding: 12px; margin-bottom: 16px; }
        .stats-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 16px; }
        .stat-card { background: #f8f9fa; border-radius: 8px; padding: 16px; text-align: center; }
        .stat-number { font-size: 2em; font-weight: 700; color: #ff9900; }
        .stat-label { font-size: 0.85em; color: #666; }
        #message { padding: 10px; border-radius: 6px; margin: 10px 0; display: none; }
        .success { background: #d4edda; color: #155724; }
        .error { background: #f8d7da; color: #721c24; }
    </style>
</head>
<body>
    <div class="header">
        <div>
            <h1>🎓 Student Record System</h1>
            <p>ICT 24267 Cloud Computing | ภาคการศึกษา 2/2568 | อ.อำนาจ คงเจริญถิ่น</p>
        </div>
    </div>
    
    <div class="container">
        <!-- API Configuration -->
        <div class="api-config">
            ⚙️ <strong>ตั้งค่า API URL:</strong>
            <input type="text" id="apiUrl" 
                   style="width:400px; margin-left:10px;"
                   placeholder="https://xxxxxxxxxx.execute-api.ap-southeast-1.amazonaws.com/prod"
                   value="">
            <button class="btn btn-primary" onclick="loadStudents()" style="margin-left:8px;">โหลดข้อมูล</button>
        </div>

        <!-- Stats -->
        <div class="card">
            <h2>📊 สถิติภาพรวม</h2>
            <div class="stats-grid">
                <div class="stat-card">
                    <div class="stat-number" id="totalStudents">-</div>
                    <div class="stat-label">นักศึกษาทั้งหมด</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number" id="avgGpa">-</div>
                    <div class="stat-label">GPA เฉลี่ย</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number" id="topGpa">-</div>
                    <div class="stat-label">GPA สูงสุด</div>
                </div>
            </div>
        </div>

        <!-- Add Student Form -->
        <div class="card">
            <h2>➕ เพิ่มนักศึกษาใหม่</h2>
            <div id="message"></div>
            <div class="form-row">
                <div class="form-group">
                    <label>รหัสนักศึกษา *</label>
                    <input type="text" id="newStudentId" placeholder="เช่น 6401006">
                </div>
                <div class="form-group">
                    <label>ชื่อ-นามสกุล *</label>
                    <input type="text" id="newName" placeholder="ชื่อภาษาไทย">
                </div>
                <div class="form-group">
                    <label>Email</label>
                    <input type="email" id="newEmail" placeholder="student@example.com">
                </div>
                <div class="form-group">
                    <label>คณะ</label>
                    <input type="text" id="newFaculty" placeholder="ICT" value="ICT">
                </div>
                <div class="form-group">
                    <label>สาขา</label>
                    <input type="text" id="newMajor" placeholder="Computer Science">
                </div>
                <div class="form-group">
                    <label>GPA</label>
                    <input type="number" id="newGpa" min="0" max="4" step="0.01" placeholder="3.50">
                </div>
            </div>
            <button class="btn btn-primary" onclick="addStudent()">เพิ่มนักศึกษา</button>
        </div>

        <!-- Student List -->
        <div class="card">
            <h2>📋 รายชื่อนักศึกษา</h2>
            <table id="studentsTable">
                <thead>
                    <tr>
                        <th>รหัสนักศึกษา</th>
                        <th>ชื่อ-นามสกุล</th>
                        <th>สาขา</th>
                        <th>GPA</th>
                        <th>จัดการ</th>
                    </tr>
                </thead>
                <tbody id="studentsBody">
                    <tr><td colspan="5" style="text-align:center">กรุณาตั้งค่า API URL แล้วกด "โหลดข้อมูล"</td></tr>
                </tbody>
            </table>
        </div>
    </div>

    <script>
        const API_URL = () => document.getElementById('apiUrl').value.replace(/\/$/, '');

        function showMessage(msg, type) {
            const el = document.getElementById('message');
            el.textContent = msg;
            el.className = type;
            el.style.display = 'block';
            setTimeout(() => el.style.display = 'none', 3000);
        }

        function getGpaBadge(gpa) {
            if (gpa >= 3.5) return `<span class="badge badge-high">${gpa}</span>`;
            if (gpa >= 2.5) return `<span class="badge badge-mid">${gpa}</span>`;
            return `<span class="badge badge-low">${gpa}</span>`;
        }

        async function loadStudents() {
            try {
                const res = await fetch(`${API_URL()}/students`);
                const data = await res.json();
                const students = data.data || [];
                
                // Update stats
                document.getElementById('totalStudents').textContent = students.length;
                if (students.length > 0) {
                    const avgGpa = students.reduce((s, st) => s + st.gpa, 0) / students.length;
                    const maxGpa = Math.max(...students.map(s => s.gpa));
                    document.getElementById('avgGpa').textContent = avgGpa.toFixed(2);
                    document.getElementById('topGpa').textContent = maxGpa.toFixed(2);
                }
                
                // Render table
                const tbody = document.getElementById('studentsBody');
                tbody.innerHTML = students.map(s => `
                    <tr>
                        <td>${s.student_id}</td>
                        <td>${s.name}</td>
                        <td>${s.major || s.faculty || '-'}</td>
                        <td>${getGpaBadge(s.gpa)}</td>
                        <td>
                            <button class="btn btn-danger" style="padding:4px 10px; font-size:0.8em"
                                onclick="deleteStudent(${s.id}, '${s.name}')">ลบ</button>
                        </td>
                    </tr>
                `).join('');
                
            } catch (err) {
                showMessage('❌ ไม่สามารถเชื่อมต่อ API ได้: ' + err.message, 'error');
            }
        }

        async function addStudent() {
            const student = {
                student_id: document.getElementById('newStudentId').value,
                name: document.getElementById('newName').value,
                email: document.getElementById('newEmail').value,
                faculty: document.getElementById('newFaculty').value,
                major: document.getElementById('newMajor').value,
                gpa: parseFloat(document.getElementById('newGpa').value) || 0
            };
            
            if (!student.student_id || !student.name) {
                showMessage('⚠️ กรุณากรอก รหัสนักศึกษา และ ชื่อ ให้ครบ', 'error');
                return;
            }
            
            try {
                const res = await fetch(`${API_URL()}/students`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(student)
                });
                const data = await res.json();
                
                if (data.status === 'success') {
                    showMessage('✅ เพิ่มนักศึกษาสำเร็จ', 'success');
                    loadStudents();
                    ['newStudentId','newName','newEmail','newMajor','newGpa'].forEach(
                        id => document.getElementById(id).value = ''
                    );
                } else {
                    showMessage('❌ ' + data.message, 'error');
                }
            } catch (err) {
                showMessage('❌ เกิดข้อผิดพลาด: ' + err.message, 'error');
            }
        }

        async function deleteStudent(id, name) {
            if (!confirm(`ยืนยันการลบ "${name}"?`)) return;
            
            try {
                const res = await fetch(`${API_URL()}/students/${id}`, { method: 'DELETE' });
                const data = await res.json();
                
                if (data.status === 'success') {
                    showMessage('✅ ลบนักศึกษาสำเร็จ', 'success');
                    loadStudents();
                }
            } catch (err) {
                showMessage('❌ เกิดข้อผิดพลาด: ' + err.message, 'error');
            }
        }
    </script>
</body>
</html>
HTMLEOF
```

```bash
# ตั้งค่า Nginx ให้ serve frontend
sudo tee /etc/nginx/conf.d/default.conf << 'EOF'
server {
    listen 80;
    server_name _;

    # Frontend
    location / {
        root /var/www/html;
        index index.html;
        try_files $uri $uri/ /index.html;
    }

    # Flask API
    location /api/ {
        proxy_pass http://127.0.0.1:5000/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
EOF

sudo systemctl reload nginx
```

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
