📚 ICT 24267 Cloud Computing: Study Guide
สรุปและเฉลย Workshop Preparation (Week 1–4)

ผู้สอน: อาจารย์อำนาจ คงเจริญถิ่น

ภาคการศึกษา: 2/2568

หัวข้อ: AWS Free Tier Workshop & Cloud Infrastructure

📑 สารบัญ (Table of Contents)
🔵 Week 1: EC2 Advanced — Web Server & Flask

🟣 Week 2: RDS — Relational Database Service

🟢 Week 3: Serverless — Lambda + DynamoDB

🟠 Week 4: Automation, Monitoring & Frontend

⚡ Quiz Cheat Sheet (จำก่อนสอบ)

🔵 Week 1: EC2 Advanced — Web Server & Flask
สร้าง Virtual Machine บน Cloud พร้อม Python Flask REST API และ Nginx Reverse Proxy

📋 Key Concepts

[x] EC2 (Elastic Compute Cloud): Virtual Machine บน AWS เลือก OS และ Size ได้

[x] Key Pair (RSA): กุญแจ SSH เข้า EC2 (.pem สำหรับ Linux/Mac, .ppk สำหรับ PuTTY)

[x] Security Group: Virtual Firewall ควบคุม Traffic ระดับ Instance

[x] User Data Script: Script ติดตั้ง Software อัตโนมัติตอนเปิดเครื่องครั้งแรก

[x] Nginx Reverse Proxy: รับ Request Port 80 แล้วส่งต่อให้ Flask Port 5000

🔌 Ports ที่ต้องจำ

Port	Protocol	การใช้งาน	Security Group (Inbound)
22	SSH	เข้าถึง Terminal	✅ จำเป็น
80	HTTP	เว็บผ่าน Nginx	✅ จำเป็น
5000	TCP	Flask Dev Server	✅ จำเป็น (ถ้าไม่ใช้ Proxy)
3306	MySQL	เชื่อมต่อ RDS	⚠️ เฉพาะภายใน
✏️ เฉลยแบบฝึกหัด & Q&A

การใช้ Nginx เป็น Reverse Proxy ดีกว่า Flask โดยตรงอย่างไร?

Security: Nginx แข็งแรงกว่า มีระบบป้องกัน DDoS และ SSL Termination

Standard: รองรับ Port 80/443 (ไม่ต้องพิมพ์ :5000 ท้าย URL)

Efficiency: Nginx จัดการ Static Files (รูปภาพ/CSS) ได้เร็วกว่า Python

🟣 Week 2: RDS — Relational Database Service
การจัดการฐานข้อมูล MySQL บน Cloud และการเชื่อมต่อกับ Flask App

📋 Key Concepts

RDS Managed Service: AWS ดูแลการ Patch และ Backup ให้ เราเขียนแค่ SQL

Environment Variables (.env): ใช้เก็บ Credentials แยกจาก Code เพื่อความปลอดภัย (ห้าม Commit ขึ้น Git!)

Parameterized Query: ใช้ %s ใน SQL เพื่อป้องกัน SQL Injection

RDS Snapshot: การ Backup แบบ Manual ที่เก็บไว้ได้ตลอดไป (ต่างจาก Automated Backup ที่มีวันหมดอายุ)

💻 Code Example: Secure Query

Python
# ✅ วิธีที่ปลอดภัย: ป้องกัน SQL Injection
cursor.execute("SELECT * FROM students WHERE name = %s", (student_name,))
🗒️ Q&A: RDS vs MySQL on EC2

หัวข้อ	RDS (Managed)	MySQL on EC2 (Self-managed)
การดูแล	AWS ดูแล Patch/Backup ให้	ต้องทำเองทั้งหมด
Scaling	กดปุ่มเพิ่มสเปกได้ทันที	ต้องย้ายข้อมูลเอง
Availability	มี Multi-AZ Failover	ต้องตั้งค่า Replication เอง
🟢 Week 3: Serverless — Lambda + DynamoDB
ระบบแบบ Event-Driven: ไม่ต้องมี Server รันค้างไว้ จ่ายเฉพาะตอนใช้งาน

📋 Key Concepts

Lambda: รัน Code เมื่อมี Event มากระตุ้น (เช่น HTTP Request)

DynamoDB: NoSQL Database (Key-Value) แบบ Serverless Scale ได้ไม่จำกัด

IAM Role: "ใบอนุญาต" ที่บอกว่า Lambda ตัวนี้มีสิทธิ์เข้าถึง Resource อะไรได้บ้าง

Cold Start: การหน่วงเวลาครั้งแรกที่รัน Lambda หลังจากไม่ได้ใช้นาน (~500ms)

📊 Comparison Table

ด้าน	DynamoDB (NoSQL)	RDS MySQL (SQL)
Schema	Flexible (ไม่มี Schema)	Fixed (ต้องกำหนด Table ล่วงหน้า)
Scaling	Scale อัตโนมัติ (High Throughput)	Scale แบบ Vertical (เพิ่มสเปกเครื่อง)
Cost	Free Tier 25 GB ตลอดไป	ฟรีเฉพาะ 12 เดือนแรก
🟠 Week 4: Automation, Monitoring & Frontend
การตั้งเวลาทำงานอัตโนมัติ และการสร้าง Dashboard ติดตามระบบ

📋 Key Concepts

EventBridge Scheduler: ตั้งเวลาทำงาน (Cron Job) เช่น cron(0 1 * * ? *) (8:00 น. เวลาไทย)

SNS (Simple Notification Service): ระบบส่งการแจ้งเตือน (Email/SMS)

S3 Static Website: การ Host เว็บ (HTML/JS) บน S3 ซึ่งถูกและ Scale ได้ดีกว่า EC2

Observability:

Logging: ดูเหตุการณ์ย้อนหลัง (CloudWatch Logs)

Monitoring: ดูสถานะปัจจุบัน (Metrics)

Alerting: แจ้งเตือนเมื่อผิดปกติ (Alarms)

📧 SNS vs SES

SNS: เหมาะสำหรับ Alert สั้นๆ (Text เท่านั้น) หรือส่งไปหลายช่องทาง

SES: เหมาะสำหรับ Email การตลาดหรือระบบที่ต้องการ HTML สวยงาม

⚡ Quiz Cheat Sheet (จำก่อนสอบ)
🚀 Services Summary

EC2: Virtual Machine จ่ายตามชั่วโมง

RDS: ฐานข้อมูล SQL (Managed)

Lambda: รัน Code ตาม Event จ่ายตาม ms

DynamoDB: NoSQL ทนทาน ฟรีตลอดไป 25GB

S3: เก็บไฟล์ และ Host Static Web

IAM: จัดการ Permission (Role/Policy)

CloudWatch: ดู Log และตั้ง Alarm

EventBridge: ตั้งเวลาทำงาน (Cron)

💡 Tips & Tricks

Security Group เป็น Stateful (อนุญาตขาเข้า ขาออกจะผ่านได้เอง)

Elastic IP จะฟรีก็ต่อเมื่อผูกกับเครื่องที่ Running อยู่เท่านั้น

t3.micro แนะนำมากกว่า t2 เพราะใช้ระบบ Nitro ที่ประสิทธิภาพดีกว่า

Principle of Least Privilege: ให้สิทธิ์น้อยที่สุดเท่าที่จำเป็นเสมอ

Prepared by: Aumnaj Khongcharoenthin (Oil)

Location: Bangkok, Thailand | Date: March 2026
