# เฉลยแบบฝึกหัด LAB Manual (AWS Workshop)
# วิชา ICT 24267 Cloud Computing
## ภาคการศึกษา 2/2568

---

| รายละเอียด | ข้อมูล |
|---|---|
| **รหัสวิชา** | ICT 24267 |
| **ชื่อวิชา** | Cloud Computing |
| **ผู้สอน** | อาจารย์อำนาจ คงเจริญถิ่น |
| **ประเภทเอกสาร** | เฉลยแบบฝึกหัดและคำถามท้ายบท |
| **หมายเหตุ** | เอกสารนี้สำหรับอาจารย์และผู้สอน — ไม่แจกจ่ายนักศึกษาก่อนส่งงาน |

---

## 📑 สารบัญ

- [Week 1 — EC2 Advanced](#-week-1--ec2-advanced-เฉลย)
  - [เฉลยแบบฝึกหัดที่ 1: เพิ่ม PUT / DELETE Endpoint](#เฉลยแบบฝึกหัดที่-1-เพิ่ม-endpoint-ใหม่)
  - [เฉลยแบบฝึกหัดที่ 2: Monitoring](#เฉลยแบบฝึกหัดที่-2-monitoring)
  - [เฉลยคำถามท้ายบท Week 1](#เฉลยคำถามท้ายบท-week-1)
- [Week 2 — RDS](#-week-2--rds-เฉลย)
  - [เฉลยแบบฝึกหัดที่ 1: Enrollment System](#เฉลยแบบฝึกหัดที่-1-enrollment-system)
  - [เฉลยแบบฝึกหัดที่ 2: RDS Snapshot](#เฉลยแบบฝึกหัดที่-2-rds-snapshot)
  - [เฉลยคำถามท้ายบท Week 2](#เฉลยคำถามท้ายบท-week-2)
- [Week 3 — Lambda & API Gateway](#-week-3--lambda--api-gateway-เฉลย)
  - [เฉลยแบบฝึกหัดที่ 1: Search Lambda Function](#เฉลยแบบฝึกหัดที่-1-lambda-function-ค้นหานักศึกษา)
  - [เฉลยแบบฝึกหัดที่ 2: API Gateway Throttling](#เฉลยแบบฝึกหัดที่-2-api-gateway-throttling)
  - [เฉลยคำถามท้ายบท Week 3](#เฉลยคำถามท้ายบท-week-3)
- [Week 4 — Integration, Security & Monitoring](#-week-4--integration-security--monitoring-เฉลย)
  - [เฉลยแบบฝึกหัดที่ 1: API Key Authentication](#เฉลยแบบฝึกหัดที่-1-api-key-authentication)
  - [เฉลยแบบฝึกหัดที่ 2: CloudWatch Logs Insights](#เฉลยแบบฝึกหัดที่-2-cloudwatch-logs-insights)
  - [เฉลยคำถามท้ายบท Week 4](#เฉลยคำถามท้ายบท-week-4)

---

---

# 📅 Week 1 — EC2 Advanced เฉลย

---

## เฉลยแบบฝึกหัดที่ 1: เพิ่ม Endpoint ใหม่

### โจทย์
เพิ่ม `PUT /students/<id>` และ `DELETE /students/<id>` ใน `app.py` (Week 1 — In-memory version)

### เฉลยโค้ดสมบูรณ์

```python
@app.route('/students/<int:student_id>', methods=['PUT'])
def update_student(student_id):
    """
    อัปเดตข้อมูลนักศึกษาตาม ID
    Request body: {"name": "...", "gpa": ...}
    Response: ข้อมูลนักศึกษาที่อัปเดตแล้ว
    """
    # ค้นหา index ของนักศึกษาใน list
    student_index = next(
        (i for i, s in enumerate(students) if s["id"] == student_id),
        None
    )

    if student_index is None:
        return jsonify({
            "status": "error",
            "message": f"Student ID {student_id} not found"
        }), 404

    data = request.get_json()
    if not data:
        return jsonify({
            "status": "error",
            "message": "Request body is required"
        }), 400

    # อัปเดตเฉพาะ field ที่ส่งมา (Partial Update)
    student = students[student_index]
    if "name" in data:
        student["name"] = data["name"]
    if "student_id" in data:
        student["student_id"] = data["student_id"]
    if "gpa" in data:
        # ตรวจสอบว่า GPA อยู่ในช่วง 0.00 - 4.00
        gpa = float(data["gpa"])
        if not (0.0 <= gpa <= 4.0):
            return jsonify({
                "status": "error",
                "message": "GPA must be between 0.00 and 4.00"
            }), 400
        student["gpa"] = gpa

    students[student_index] = student

    return jsonify({
        "status": "success",
        "message": "Student updated successfully",
        "data": student
    })


@app.route('/students/<int:student_id>', methods=['DELETE'])
def delete_student(student_id):
    """
    ลบข้อมูลนักศึกษาตาม ID
    Response: {"status": "success", "message": "Student deleted"}
    """
    global students

    # ค้นหานักศึกษาที่ต้องการลบ
    student = next((s for s in students if s["id"] == student_id), None)

    if student is None:
        return jsonify({
            "status": "error",
            "message": f"Student ID {student_id} not found"
        }), 404

    # ลบออกจาก list
    students = [s for s in students if s["id"] != student_id]

    return jsonify({
        "status": "success",
        "message": f"Student '{student['name']}' (ID: {student_id}) deleted successfully"
    })
```

### คำสั่งทดสอบ

```bash
PUBLIC_IP="<YOUR_PUBLIC_IP>"

# ทดสอบ PUT — อัปเดต GPA นักศึกษา ID 1
curl -X PUT http://$PUBLIC_IP:5000/students/1 \
  -H "Content-Type: application/json" \
  -d '{"name": "สมชาย ใจดีมาก", "gpa": 3.75}'

# ทดสอบ PUT — ส่ง ID ที่ไม่มีอยู่ (ต้องได้ 404)
curl -X PUT http://$PUBLIC_IP:5000/students/999 \
  -H "Content-Type: application/json" \
  -d '{"name": "ไม่มีคนนี้"}'

# ทดสอบ DELETE — ลบนักศึกษา ID 2
curl -X DELETE http://$PUBLIC_IP:5000/students/2

# ตรวจสอบว่าลบแล้วจริง (ต้องเห็นแค่ 1 คน)
curl http://$PUBLIC_IP:5000/students

# ทดสอบ DELETE ซ้ำ (ต้องได้ 404)
curl -X DELETE http://$PUBLIC_IP:5000/students/2
```

### ผลลัพธ์ที่คาดหวัง

```json
// PUT สำเร็จ
{
  "status": "success",
  "message": "Student updated successfully",
  "data": {"id": 1, "name": "สมชาย ใจดีมาก", "student_id": "6401001", "gpa": 3.75}
}

// DELETE สำเร็จ
{
  "status": "success",
  "message": "Student 'สมหญิง รักเรียน' (ID: 2) deleted successfully"
}

// กรณี ID ไม่มีอยู่ (404)
{
  "status": "error",
  "message": "Student ID 999 not found"
}
```

> 💡 **จุดที่นักศึกษามักทำผิด**: ลืมใช้ `global students` ใน delete function เมื่อต้องการแทนที่ list ทั้งหมด หากไม่ใส่ `global` Python จะมองว่าเป็นตัวแปร local และ list ต้นฉบับจะไม่เปลี่ยนแปลง

---

## เฉลยแบบฝึกหัดที่ 2: Monitoring

### โจทย์
ทดลอง stress test และสังเกต CloudWatch Metrics

### เฉลยและค่าที่ควรสังเกต

```bash
# SSH เข้า EC2 แล้วรัน
sudo yum install -y stress

# รัน CPU stress 60 วินาที (1 core)
stress --cpu 1 --timeout 60 &

# ระหว่างรัน ดู CPU realtime
top
# หรือ
watch -n 1 'ps aux | grep stress'
```

**ค่าที่ควรบันทึกและเปรียบเทียบ:**

| Metric | ก่อน stress | ระหว่าง stress | หลัง stress |
|---|---|---|---|
| CPU Utilization | ~5–10% | ~90–100% | ~5–10% |
| Network In | ต่ำ | ต่ำ (stress ไม่ใช้ network) | ต่ำ |
| Status Check | Passed | Passed | Passed |

**ข้อสังเกตสำคัญ:**
- CloudWatch Metrics มี delay ประมาณ **1–5 นาที** จึงจะเห็นการเปลี่ยนแปลงใน Console
- t2.micro มี **CPU Credits** — หากใช้ CPU สูงนานเกินไปจะหมด Credit และ Performance จะลดลง
- ดูจำนวน CPU Credits ได้จาก Metric `CPUCreditBalance`

---

## เฉลยคำถามท้ายบท Week 1

**ข้อที่ 1. t2.micro vs t3.micro ต่างกันอย่างไร?**

> **เฉลย:** ทั้งคู่เป็น Burstable Performance Instances แต่ต่างกันดังนี้:
> - **t2.micro**: รุ่นเก่า, ใช้ Intel CPU, CPU Credit สะสมช้ากว่า, ไม่รองรับ Unlimited Mode ด้วยค่าเริ่มต้น
> - **t3.micro**: รุ่นใหม่กว่า, ใช้ Intel หรือ AMD CPU, สะสม CPU Credit เร็วกว่า, รองรับ **Unlimited Burst Mode** โดย default (แต่อาจมีค่าใช้จ่ายเพิ่มหากใช้ CPU เกิน limit นาน), ราคาถูกกว่า t2.micro ในบางกรณี
> - AWS แนะนำ **t3.micro** สำหรับ workload ใหม่เพราะมีประสิทธิภาพดีกว่าในราคาเท่ากันหรือถูกกว่า

---

**ข้อที่ 2. Inbound vs Outbound rules**

> **เฉลย:**
> - **Inbound rules**: ควบคุม traffic ที่เข้ามาหา Instance เช่น อนุญาต Port 22 (SSH) เฉพาะจาก IP ของเรา, อนุญาต Port 80 จากทุกที่
> - **Outbound rules**: ควบคุม traffic ที่ออกจาก Instance เช่น Instance จะส่ง request ออกไปไหนได้บ้าง
> - Security Group เป็น **Stateful** คือถ้าอนุญาต Inbound แล้ว Response ของมันจะ allow กลับออกไปอัตโนมัติโดยไม่ต้องตั้ง Outbound
> - **ความสำคัญของ Outbound**: ในระบบที่ปลอดภัยสูง ควรจำกัด Outbound เช่น ไม่ให้ EC2 ติดต่อ IP ภายนอกที่ไม่รู้จัก เพื่อป้องกัน **Data Exfiltration** กรณีถูก Compromise

---

**ข้อที่ 3. User Data vs SSH**

> **เฉลย:**
>
> | | User Data | SSH Manual |
> |---|---|---|
> | **ข้อดี** | Automated, Reproducible, เหมาะกับ Infrastructure as Code | ยืดหยุ่น, แก้ไขง่าย, เห็น output realtime |
> | **ข้อเสีย** | Debug ยาก, ทำงานครั้งเดียว, ต้อง launch ใหม่หากผิดพลาด | ไม่ automated, ทำซ้ำยาก, Human error สูง |
> | **เหมาะกับ** | Production, Auto Scaling, Infrastructure as Code | Development, One-time tasks, Debugging |

---

**ข้อที่ 4. ลืม Release Elastic IP**

> **เฉลย:** หาก **Allocate Elastic IP แล้วไม่ได้ Associate** กับ Running Instance AWS จะเรียกเก็บ **$0.005 ต่อชั่วโมง** (~$3.60/เดือน) เพราะถือว่าเป็นการ waste ทรัพยากร IP สาธารณะ
>
> **วิธีหลีกเลี่ยง:**
> 1. ตั้ง **Billing Alert** เมื่อค่าใช้จ่ายเกิน $0
> 2. ตรวจสอบ Elastic IPs ใน Console เสมอก่อนออกจากระบบ
> 3. หากไม่ใช้งาน ให้ **Disassociate** แล้ว **Release** ทันที
> 4. ใช้ **AWS Cost Explorer** เพื่อดูค่าใช้จ่ายรายวัน

---

**ข้อที่ 5. ทำไมต้องใช้ Nginx หน้า Flask**

> **เฉลย:** Flask dev server มีข้อจำกัดหลายประการสำหรับ Production:
> 1. **Performance**: Flask dev server รองรับ request ได้ทีละ 1 ใน 1 thread, Nginx รองรับ concurrent connections ได้หลายหมื่น
> 2. **Static Files**: Nginx serve static files (HTML, CSS, JS, Images) ได้เร็วกว่า Flask มาก
> 3. **Security**: Nginx ทำหน้าที่ Buffer ป้องกัน Slowloris attack, ซ่อน Flask version/stack
> 4. **SSL/TLS**: ติดตั้ง HTTPS ที่ Nginx layer ได้โดยไม่ต้องแก้ Flask code
> 5. **Process Isolation**: Flask crash ไม่กระทบ Nginx ผู้ใช้ยังเห็น error page แทน connection refused

---

---

# 📅 Week 2 — RDS เฉลย

---

## เฉลยแบบฝึกหัดที่ 1: Enrollment System

### โจทย์
เพิ่ม 3 Endpoints: `POST /enrollments`, `GET /students/<id>/courses`, `GET /courses/<id>/students`

### เฉลยโค้ดสมบูรณ์

เพิ่มใน `app.py` (Week 2 Version):

```python
# ============================================================
# ENROLLMENT ENDPOINTS
# ============================================================

@app.route('/enrollments', methods=['POST'])
def create_enrollment():
    """
    ลงทะเบียนนักศึกษาในวิชา
    Request body: {"student_id": 1, "course_id": 1, "semester": "2/2568"}
    """
    try:
        data = request.get_json()

        # Validate required fields
        required = ['student_id', 'course_id']
        for field in required:
            if not data.get(field):
                return jsonify({
                    "status": "error",
                    "message": f"Missing required field: {field}"
                }), 400

        # ตรวจสอบว่า student มีอยู่จริง
        student = execute_query(
            "SELECT id, name FROM students WHERE id = %s",
            (data['student_id'],)
        )
        if not student:
            return jsonify({
                "status": "error",
                "message": f"Student ID {data['student_id']} not found"
            }), 404

        # ตรวจสอบว่า course มีอยู่จริง
        course = execute_query(
            "SELECT id, course_name FROM courses WHERE id = %s",
            (data['course_id'],)
        )
        if not course:
            return jsonify({
                "status": "error",
                "message": f"Course ID {data['course_id']} not found"
            }), 404

        # ตรวจสอบว่าลงทะเบียนซ้ำหรือไม่ (Duplicate check)
        existing = execute_query(
            """SELECT id FROM enrollments
               WHERE student_id = %s AND course_id = %s AND semester = %s""",
            (data['student_id'], data['course_id'], data.get('semester', ''))
        )
        if existing:
            return jsonify({
                "status": "error",
                "message": "Student is already enrolled in this course for this semester"
            }), 409  # 409 Conflict

        # บันทึก enrollment
        new_id = execute_query(
            """INSERT INTO enrollments (student_id, course_id, grade, semester)
               VALUES (%s, %s, %s, %s)""",
            (
                data['student_id'],
                data['course_id'],
                data.get('grade', None),
                data.get('semester', '2/2568')
            ),
            fetch=False
        )

        return jsonify({
            "status": "success",
            "message": f"Enrolled '{student[0]['name']}' in '{course[0]['course_name']}'",
            "data": {
                "enrollment_id": new_id,
                "student_id": data['student_id'],
                "course_id": data['course_id'],
                "semester": data.get('semester', '2/2568')
            }
        }), 201

    except Exception as e:
        return jsonify({"status": "error", "message": str(e)}), 500


@app.route('/students/<int:student_id>/courses', methods=['GET'])
def get_student_courses(student_id):
    """
    ดูวิชาทั้งหมดที่นักศึกษาลงทะเบียน
    """
    try:
        # ตรวจสอบว่า student มีอยู่
        student = execute_query(
            "SELECT id, name, student_id FROM students WHERE id = %s",
            (student_id,)
        )
        if not student:
            return jsonify({
                "status": "error",
                "message": f"Student ID {student_id} not found"
            }), 404

        # ดึงวิชาที่ลงทะเบียนพร้อม JOIN
        courses = execute_query(
            """SELECT
                e.id AS enrollment_id,
                c.course_code,
                c.course_name,
                c.credits,
                c.instructor,
                e.grade,
                e.semester
               FROM enrollments e
               JOIN courses c ON e.course_id = c.id
               WHERE e.student_id = %s
               ORDER BY e.semester, c.course_code""",
            (student_id,)
        )

        return jsonify({
            "status": "success",
            "student": {
                "id": student[0]['id'],
                "name": student[0]['name'],
                "student_id": student[0]['student_id']
            },
            "enrolled_courses": len(courses),
            "data": courses
        })

    except Exception as e:
        return jsonify({"status": "error", "message": str(e)}), 500


@app.route('/courses/<int:course_id>/students', methods=['GET'])
def get_course_students(course_id):
    """
    ดูนักศึกษาทั้งหมดในวิชา
    """
    try:
        # ตรวจสอบว่า course มีอยู่
        course = execute_query(
            "SELECT id, course_code, course_name FROM courses WHERE id = %s",
            (course_id,)
        )
        if not course:
            return jsonify({
                "status": "error",
                "message": f"Course ID {course_id} not found"
            }), 404

        # ดึงนักศึกษาในวิชาพร้อม JOIN
        students = execute_query(
            """SELECT
                s.id,
                s.student_id,
                s.name,
                s.faculty,
                s.major,
                s.gpa,
                e.grade,
                e.semester
               FROM enrollments e
               JOIN students s ON e.student_id = s.id
               WHERE e.course_id = %s
               ORDER BY s.student_id""",
            (course_id,)
        )

        # แปลง Decimal เป็น float
        for s in students:
            s['gpa'] = float(s['gpa']) if s['gpa'] else 0.0

        return jsonify({
            "status": "success",
            "course": {
                "id": course[0]['id'],
                "code": course[0]['course_code'],
                "name": course[0]['course_name']
            },
            "total_students": len(students),
            "data": students
        })

    except Exception as e:
        return jsonify({"status": "error", "message": str(e)}), 500
```

### คำสั่งทดสอบ

```bash
BASE_URL="http://<YOUR_PUBLIC_IP>:5000"

# ลงทะเบียนนักศึกษา ID 1 ในวิชา ID 1
curl -X POST $BASE_URL/enrollments \
  -H "Content-Type: application/json" \
  -d '{"student_id": 1, "course_id": 1, "semester": "2/2568"}'

# ลงทะเบียนซ้ำ (ต้องได้ 409 Conflict)
curl -X POST $BASE_URL/enrollments \
  -H "Content-Type: application/json" \
  -d '{"student_id": 1, "course_id": 1, "semester": "2/2568"}'

# ดูวิชาที่นักศึกษา ID 1 ลงทะเบียน
curl $BASE_URL/students/1/courses

# ดูนักศึกษาในวิชา ID 1
curl $BASE_URL/courses/1/students
```

> 💡 **จุดสำคัญในเฉลย**: การ Validate ทั้ง student และ course ก่อน INSERT และการตรวจสอบ Duplicate enrollment เป็น Best Practice ที่ป้องกัน Data Integrity ปัญหา

---

## เฉลยแบบฝึกหัดที่ 2: RDS Snapshot

### โจทย์
สร้าง Manual Snapshot และตรวจสอบ

### ขั้นตอนสมบูรณ์และสิ่งที่ต้องสังเกต

```
1. RDS Console → Databases → ict24267-db
2. Actions → Take snapshot
3. Snapshot identifier: ict24267-db-week2-backup
4. Take Snapshot → รอจนสถานะเป็น "Available"
```

**สิ่งที่นักศึกษาควรบันทึก:**

| รายการ | ค่าที่พบ |
|---|---|
| Snapshot Identifier | ict24267-db-week2-backup |
| Snapshot Type | Manual |
| Status | Available |
| Snapshot Creation Time | (บันทึกเวลาจริง) |
| Allocated Storage | 20 GB |
| Engine Version | MySQL 8.0.x |

**ทดสอบเพิ่มเติม — Restore จาก Snapshot (ถ้าเวลาพอ):**
```
1. RDS → Snapshots → เลือก Snapshot → Actions → Restore snapshot
2. DB Instance Identifier: ict24267-db-restore-test
3. Instance class: db.t3.micro
4. Single-AZ
5. Restore DB Instance
6. หลัง restore สำเร็จ → ลบ Instance ทิ้ง (เพื่อไม่ให้เกิดค่าใช้จ่าย)
```

> ⚠️ **ข้อควรระวัง**: Snapshot ที่ยังไม่ลบจะมีค่าใช้จ่าย Storage ($0.095/GB/เดือน) หลังจาก Free Tier หมด ควรลบ Snapshot ที่ไม่จำเป็นออก

---

## เฉลยคำถามท้ายบท Week 2

**ข้อที่ 1. RDS Managed Service vs MySQL บน EC2 (อย่างน้อย 3 ข้อ)**

> **เฉลย:**
> 1. **Automated Backups**: RDS จัดการ Backup อัตโนมัติ, Point-in-time Recovery ได้ถึงระดับวินาที — MySQL บน EC2 ต้องเขียน Script จัดการเอง
> 2. **Patching & Maintenance**: AWS อัปเดต OS และ Database Engine ให้อัตโนมัติในช่วง Maintenance Window — EC2 ต้อง patch เอง ซึ่งเสี่ยงต่อการลืมและ Security Vulnerability
> 3. **High Availability**: เปิด Multi-AZ ได้ด้วย 1 คลิก มี Automatic Failover — EC2 ต้องติดตั้ง MySQL Replication เองซึ่งซับซ้อนมาก
> 4. **Monitoring**: มี Performance Insights, Enhanced Monitoring รวมอยู่แล้ว
> 5. **Scalability**: เพิ่ม Instance Size ได้ง่ายโดย Downtime น้อย

---

**ข้อที่ 2. ทำไมตั้ง `Public access: No`**

> **เฉลย:** Database เป็น Layer ที่สำคัญที่สุดของระบบ ถ้าเปิด Public Access:
> - Attacker สามารถพยายาม **Brute Force** Password MySQL โดยตรงจาก Internet
> - เสี่ยงต่อ **Credential Stuffing** โดยใช้ password ที่ Leak จากที่อื่น
> - เสี่ยงต่อ **Zero-day exploits** ของ MySQL ที่ยังไม่ได้ Patch
>
> การให้ EC2 เป็น Gateway สร้าง **Defense in Depth** — ผู้โจมตีต้องผ่าน EC2 ก่อน (ซึ่งมี Security Group, SSH Key, OS firewall) จึงจะเข้าถึง RDS ได้

---

**ข้อที่ 3. Connection Pooling**

> **เฉลย:** ปัญหาของการสร้าง Connection ใหม่ทุก Request:
> - MySQL มี **max_connections** จำกัด (default 151) — 1,000 users พร้อมกันจะทำให้ Connection หมดและ Error `Too many connections`
> - การสร้าง TCP Connection + MySQL Handshake ใช้เวลา **10–100ms** ต่อครั้ง ทำให้ Response ช้า
>
> **Connection Pool** แก้ปัญหาโดย:
> - เปิด Connection ไว้ล่วงหน้าจำนวนหนึ่ง (เช่น 10 connections)
> - Request ที่เข้ามา **ยืม** connection ที่ว่างอยู่ใช้ แทนการสร้างใหม่
> - ใช้ Library เช่น `SQLAlchemy` หรือ `DBUtils` ใน Python

---

**ข้อที่ 4. RDS Backup กี่แบบ**

> **เฉลย:** AWS RDS มี Backup 2 แบบหลัก:
>
> | | Automated Backup | Manual Snapshot |
> |---|---|---|
> | **ทริกเกอร์** | อัตโนมัติทุกวัน | Manual โดย User หรือ Script |
> | **Retention** | 1–35 วัน (กำหนดได้) | เก็บถาวรจนกว่าจะลบ |
> | **Point-in-time** | ได้ (Transaction Log + Daily Backup) | ไม่ได้ (เฉพาะเวลาที่ Snapshot) |
> | **ลบอัตโนมัติ** | ใช่ เมื่อถึง Retention Period | ไม่ — ต้อง Delete เอง |
> | **Free Tier** | Storage ฟรีเท่า DB size | นับรวม Free Storage 20 GB |

---

**ข้อที่ 5. SQL Injection และ Parameterized Query**

> **เฉลย:**
>
> **ตัวอย่าง String Formatting ที่อันตราย:**
> ```python
> # อันตราย!
> student_id = request.args.get('id')
> query = f"SELECT * FROM students WHERE id = {student_id}"
> # ถ้า student_id = "1 OR 1=1" → ดึงข้อมูลทั้งหมด
> # ถ้า student_id = "1; DROP TABLE students; --" → ลบ Table ทิ้ง!
> ```
>
> **Parameterized Query ปลอดภัยเพราะ:**
> ```python
> # ปลอดภัย
> cursor.execute("SELECT * FROM students WHERE id = %s", (student_id,))
> # MySQL Driver จะ escape ค่าใน student_id ก่อนส่ง
> # "1 OR 1=1" จะถูกมองเป็น string literal ไม่ใช่ SQL command
> ```
> MySQL Driver จะแยก **SQL Structure** ออกจาก **Data** ทำให้ Input ของผู้ใช้ไม่มีทางเปลี่ยน Logic ของ Query ได้

---

---

# 📅 Week 3 — Lambda & API Gateway เฉลย

---

## เฉลยแบบฝึกหัดที่ 1: Lambda Function ค้นหานักศึกษา

### โจทย์
สร้าง `ict24267-search-students` ที่รับ `keyword` และค้นหาจาก `name` และ `student_id`

### เฉลยโค้ดสมบูรณ์

```python
# lambda_search_students.py
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

def lambda_handler(event, context):
    """
    ค้นหานักศึกษาจาก keyword
    Query param: ?keyword=สมชาย หรือ ?keyword=6401
    """
    logger.info(f"Search event: {json.dumps(event)}")

    query_params = event.get('queryStringParameters') or {}
    keyword = query_params.get('keyword', '').strip()

    # Validate: keyword ต้องมีความยาวอย่างน้อย 2 ตัวอักษร
    if not keyword:
        return build_response(400, {
            "status": "error",
            "message": "Query parameter 'keyword' is required"
        })

    if len(keyword) < 2:
        return build_response(400, {
            "status": "error",
            "message": "Keyword must be at least 2 characters long"
        })

    conn = None
    try:
        conn = get_db_connection()

        with conn.cursor() as cursor:
            # ค้นหาจากทั้ง name, student_id และ email
            # ใช้ Parameterized Query เพื่อป้องกัน SQL Injection
            search_pattern = f"%{keyword}%"

            cursor.execute(
                """SELECT id, student_id, name, email, faculty, major, gpa
                   FROM students
                   WHERE name LIKE %s
                      OR student_id LIKE %s
                      OR email LIKE %s
                   ORDER BY
                       CASE
                           WHEN student_id = %s THEN 1
                           WHEN name LIKE %s THEN 2
                           ELSE 3
                       END,
                       student_id""",
                (
                    search_pattern,   # name LIKE
                    search_pattern,   # student_id LIKE
                    search_pattern,   # email LIKE
                    keyword,          # exact student_id match (rank 1)
                    f"{keyword}%"     # name starts with keyword (rank 2)
                )
            )

            results = cursor.fetchall()

            # แปลง Decimal เป็น float
            for r in results:
                r['gpa'] = float(r['gpa']) if r['gpa'] else 0.0

        return build_response(200, {
            "status": "success",
            "keyword": keyword,
            "total_found": len(results),
            "data": results
        })

    except pymysql.Error as e:
        logger.error(f"DB Error: {str(e)}")
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
    return {
        "statusCode": status_code,
        "headers": {
            "Content-Type": "application/json",
            "Access-Control-Allow-Origin": "*",
            "Access-Control-Allow-Headers": "Content-Type",
            "Access-Control-Allow-Methods": "GET,OPTIONS"
        },
        "body": json.dumps(body, ensure_ascii=False, default=str)
    }
```

### เพิ่ม Route ใน API Gateway

```
API Gateway → ict24267-student-api
→ Resources → /students → Actions → Create Resource
→ Resource Name: search
→ Resource Path: search
→ Create Resource

→ เลือก /students/search → Create Method → GET
→ Lambda Function: ict24267-search-students
→ Save

→ Deploy API → prod stage
```

### คำสั่งทดสอบ

```bash
API_URL="https://xxxxxxxxxx.execute-api.ap-southeast-1.amazonaws.com/prod"

# ค้นหาด้วยชื่อ
curl "$API_URL/students/search?keyword=สมชาย"

# ค้นหาด้วยรหัสนักศึกษา
curl "$API_URL/students/search?keyword=6401"

# ค้นหาที่สั้นเกินไป (ต้องได้ 400)
curl "$API_URL/students/search?keyword=ส"

# ไม่ส่ง keyword (ต้องได้ 400)
curl "$API_URL/students/search"
```

### ผลลัพธ์ที่คาดหวัง

```json
{
  "status": "success",
  "keyword": "สมชาย",
  "total_found": 1,
  "data": [
    {
      "id": 1,
      "student_id": "6401001",
      "name": "สมชาย ใจดี",
      "email": "somchai@example.com",
      "faculty": "ICT",
      "major": "Computer Science",
      "gpa": 3.5
    }
  ]
}
```

> 💡 **จุดที่น่าสนใจในเฉลย**: การใช้ `CASE WHEN` ใน `ORDER BY` เพื่อ Rank ผลลัพธ์ที่ตรงกับ keyword มากกว่าให้ขึ้นก่อน เป็น Pattern ที่ใช้บ่อยในระบบค้นหาจริง

---

## เฉลยแบบฝึกหัดที่ 2: API Gateway Throttling

### โจทย์
ตั้ง Throttling และอธิบายประโยชน์

### ขั้นตอนสมบูรณ์

```
1. API Gateway → ict24267-student-api
2. Stages → prod
3. Default Method Throttling: เปิด Enable throttling
4. Rate: 100 (requests/second)
5. Burst: 200 (maximum concurrent requests)
6. Save Changes
```

### คำอธิบายที่นักศึกษาควรให้

**Throttling ใน API Gateway มีประโยชน์ดังนี้:**

1. **ป้องกัน DDoS / Abuse**: จำกัดจำนวน Request ต่อวินาที ป้องกันผู้ไม่ประสงค์ดี Flood API จนล่ม
2. **ปกป้อง Backend (Lambda/RDS)**: Lambda มี Concurrent Execution limit, RDS มี Connection limit — Throttling ป้องกันไม่ให้ Backend รับงานเกินกว่าจะรับไหว
3. **Cost Control**: Lambda คิดค่า Request และ Duration — Throttling ช่วยจำกัดค่าใช้จ่ายกรณีเกิด Bug วน loop เรียก API
4. **Fair Usage**: ในระบบที่มีหลาย Client ป้องกัน Client คนใดคนหนึ่งเรียก API มากเกินสัดส่วน

**ความแตกต่าง Rate vs Burst:**
- **Rate** = จำนวน Request สูงสุดต่อวินาที (Steady-state)
- **Burst** = จำนวน Request สูงสุดที่รับได้ใน Spike ชั่วคราว (Token Bucket)

---

## เฉลยคำถามท้ายบท Week 3

**ข้อที่ 1. Cold Start คืออะไร และแก้ไขอย่างไร**

> **เฉลย:** Cold Start เกิดขึ้นเมื่อ Lambda ถูก Invoke และไม่มี Warm Container รอรับงาน AWS ต้องทำ:
> 1. สร้าง Container ใหม่
> 2. ดาวน์โหลด Deployment Package
> 3. Initialize Runtime (Python interpreter)
> 4. รัน Initialization Code (นอก handler)
>
> ใช้เวลา **200ms–2s** ขึ้นอยู่กับขนาด Package และ VPC
>
> **วิธีแก้ไข:**
> - **Provisioned Concurrency**: จ่ายเงินให้ AWS Keep Warm Container ไว้ตลอด (มีค่าใช้จ่าย)
> - **Scheduled Warm-up**: ใช้ EventBridge ping Lambda ทุก 5 นาที (ฟรี แต่ไม่ Reliable)
> - **ลดขนาด Package**: ยิ่ง Package เล็ก Cold Start ยิ่งเร็ว — ใช้ Layers แยก Dependencies
> - **เลี่ยง VPC**: Lambda ใน VPC Cold Start ช้ากว่าปกติเพราะต้อง attach ENI (แต่ AWS ปรับปรุงแล้วใน 2019+)

---

**ข้อที่ 2. Lambda vs EC2 สำหรับ Student Record System**

> **เฉลย:**
>
> | | EC2 + Flask | Lambda + API Gateway |
> |---|---|---|
> | **Cost (Low Traffic)** | จ่ายตลอด 24 ชม. แม้ไม่มี Request | จ่ายเฉพาะตอนมี Request |
> | **Cost (High Traffic)** | Fixed Cost เดิม | อาจแพงกว่าถ้า Traffic สูงมาก |
> | **Scalability** | ต้อง Manual หรือ Auto Scaling Group | Scale อัตโนมัติไม่จำกัด |
> | **Maintenance** | ต้อง Patch OS, Manage Server | AWS จัดการทั้งหมด |
> | **Cold Start** | ไม่มี | มี (200ms–2s) |
> | **Max Execution** | ไม่จำกัด | 15 นาที |
> | **เหมาะกับ** | Traffic สม่ำเสมอ, Long-running tasks | Traffic ไม่แน่นอน, Microservices |

---

**ข้อที่ 3. VPC Lambda**

> **เฉลย:** RDS ที่ตั้งค่า `Public accessibility: No` จะมี Endpoint ที่เข้าถึงได้เฉพาะจาก **Private IP ภายใน VPC** เท่านั้น
>
> Lambda ที่ไม่ได้อยู่ใน VPC จะรันใน **AWS-managed VPC** ที่แยกต่างหาก ไม่สามารถ Route ไปหา Private IP ของ RDS ใน User VPC ได้
>
> **ผลต่อ Cold Start**: Lambda ใน VPC เดิมต้องสร้าง **ENI (Elastic Network Interface)** ใหม่ทุก Cold Start ใช้เวลาเพิ่ม 10+ วินาที แต่ตั้งแต่ปี 2019 AWS เปลี่ยนมาใช้ **Hyperplane ENI** ที่ Share กันระหว่าง Lambda functions ทำให้ Cold Start ใน VPC เร็วขึ้นมาก

---

**ข้อที่ 4. REST API vs HTTP API ใน API Gateway**

> **เฉลย:**
>
> | | REST API | HTTP API |
> |---|---|---|
> | **ราคา** | แพงกว่า | ถูกกว่า ~70% |
> | **Features** | ครบ: Usage Plans, API Keys, Request Validation, WAF, Caching | พื้นฐาน: JWT Auth, CORS |
> | **Latency** | สูงกว่าเล็กน้อย | ต่ำกว่า |
> | **เหมาะกับ** | Production API ที่ต้องการ Rate Limiting, Caching, Request Transformation | Simple Proxy, Internal API, ต้องการ Cost ต่ำ |
>
> **แนะนำสำหรับ LAB**: HTTP API ถ้าต้องการประหยัดค่าใช้จ่าย, REST API ถ้าต้องการ API Keys และ Usage Plan

---

**ข้อที่ 5. Idempotency สำหรับ POST /students**

> **เฉลย:** Idempotency คือการที่ Request เดิมส่งซ้ำหลายครั้งได้ผลลัพธ์เหมือนส่งครั้งเดียว
>
> **ปัญหา**: ถ้า Client ส่ง `POST /students` แล้ว Network หลุดก่อนได้ Response — Client ไม่รู้ว่า Server ทำงานสำเร็จหรือไม่ จึงส่งซ้ำ ทำให้เกิดข้อมูลซ้ำ
>
> **วิธี Implement:**
> ```python
> # วิธีที่ 1: ตรวจสอบ Unique Key ใน Database
> # student_id เป็น UNIQUE ใน MySQL อยู่แล้ว → INSERT จะ fail พร้อม error ที่ชัดเจน
>
> # วิธีที่ 2: Idempotency Key Header
> idempotency_key = request.headers.get('Idempotency-Key')
> # เก็บ key ใน Cache (Redis/DynamoDB) พร้อม Response
> # ถ้า key ซ้ำ → Return cached response แทนการ INSERT ใหม่
> ```
> วิธีที่ 1 เหมาะกับ LAB เพราะใช้ `UNIQUE constraint` บน `student_id` ใน MySQL อยู่แล้ว

---

---

# 📅 Week 4 — Integration, Security & Monitoring เฉลย

---

## เฉลยแบบฝึกหัดที่ 1: API Key Authentication

### โจทย์
เพิ่ม API Key Authentication บน API Gateway

### ขั้นตอนสมบูรณ์

```
ขั้นตอนที่ 1: สร้าง API Key
─────────────────────────────
API Gateway → API Keys → Create API Key
Name: ict24267-student-apikey
Description: API Key for ICT24267 Student System
Enabled: ✅
Auto Generate: ✅ (หรือกำหนดค่าเอง)
Save

ขั้นตอนที่ 2: สร้าง Usage Plan
─────────────────────────────
API Gateway → Usage Plans → Create
Name: ict24267-usage-plan
Description: Usage plan for ICT24267
Throttling:
  Rate: 100 req/sec
  Burst: 200 req
Quota:
  1000 requests per Day ✅
Create and add stages → ict24267-student-api / prod
Next → Add API Key → ict24267-student-apikey
Done

ขั้นตอนที่ 3: เปิดใช้ API Key บน Method
─────────────────────────────
API Gateway → ict24267-student-api → Resources
เลือก GET บน /students → Method Request
API Key Required: true ✅
Save

ทำซ้ำกับทุก Method ที่ต้องการ (POST, PUT, DELETE)

ขั้นตอนที่ 4: Deploy ซ้ำ
─────────────────────────────
Actions → Deploy API → prod
```

### ทดสอบ

```bash
API_URL="https://xxxxxxxxxx.execute-api.ap-southeast-1.amazonaws.com/prod"
API_KEY="xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# เรียกโดยไม่มี API Key (ต้องได้ 403 Forbidden)
curl $API_URL/students

# เรียกพร้อม API Key (ต้องสำเร็จ)
curl $API_URL/students \
  -H "x-api-key: $API_KEY"

# POST พร้อม API Key
curl -X POST $API_URL/students \
  -H "Content-Type: application/json" \
  -H "x-api-key: $API_KEY" \
  -d '{"student_id": "6401099", "name": "ทดสอบ Key", "gpa": 3.0}'
```

### ผลลัพธ์ที่คาดหวัง

```json
// ไม่มี API Key → 403
{
  "message": "Forbidden"
}

// มี API Key ถูกต้อง → 200
{
  "status": "success",
  "count": 3,
  "data": [...]
}
```

> 💡 **หมายเหตุ**: API Key ใน API Gateway ไม่ใช่ Authentication ที่แข็งแกร่ง เป็นเพียง Identification — สำหรับ Production ควรใช้ **JWT + Cognito** หรือ **IAM Authorization** แทน

---

## เฉลยแบบฝึกหัดที่ 2: CloudWatch Logs Insights

### โจทย์
รัน Query ใน CloudWatch Logs Insights

### วิธีเข้าถึงและผลลัพธ์ที่ควรเห็น

```
CloudWatch → Logs Insights
Log groups: เลือก /aws/lambda/ict24267-get-students
Time range: Last 1 hour
```

**Query 1: ดู Lambda Errors**
```
fields @timestamp, @message
| filter @message like /ERROR/
| sort @timestamp desc
| limit 20
```

ผลลัพธ์ที่ควรเห็น (ถ้าไม่มี Error จะเป็น Empty Result):
```
No results found for the specified time range.
```
หรือถ้ามี Error:
```
@timestamp              @message
2568-xx-xx 10:23:45    ERROR Database error: Can't connect to MySQL server
```

---

**Query 2: ดู Response Time ของ Lambda**
```
fields @timestamp, @duration
| filter @type = "REPORT"
| stats avg(@duration), max(@duration) by bin(5m)
```

ผลลัพธ์ตัวอย่าง:
```
bin(5m)                  avg(@duration)   max(@duration)
2568-xx-xx 10:00:00     245.32 ms        1243.00 ms   ← Cold Start
2568-xx-xx 10:05:00     87.45 ms         156.00 ms    ← Warm
2568-xx-xx 10:10:00     92.10 ms         201.00 ms    ← Warm
```

**สิ่งที่นักศึกษาควรสังเกต:**
- ค่า `max(@duration)` ที่สูงผิดปกติในช่วงแรก → **Cold Start**
- ค่า `avg(@duration)` หลังจากนั้นต่ำลงมาก → **Warm Execution**
- Lambda ที่เชื่อม VPC จะมี max duration สูงกว่า Lambda ทั่วไปในช่วง Cold Start

**Query เพิ่มเติมที่น่าสนใจ:**
```
# ดูจำนวน Request ต่อนาที
filter @type = "REPORT"
| stats count(*) as requestCount by bin(1m)
| sort bin(1m) asc

# ดู Memory ที่ใช้จริงเทียบกับที่จัดสรร
filter @type = "REPORT"
| stats
    avg(@maxMemoryUsed) as avgMemUsed,
    avg(@memorySize) as allocated,
    max(@maxMemoryUsed) as peakMem
```

---

## เฉลยคำถามท้ายบท Week 4

**ข้อที่ 1. Architecture Decision: EC2+Flask vs Lambda+API Gateway**

> **เฉลย (แนวทางการตอบ — ไม่มีคำตอบถูกผิด 100%):**
>
> **เลือก Lambda + API Gateway เมื่อ:**
> - Traffic ไม่แน่นอน มี Spike บางช่วง (เช่น ช่วงลงทะเบียน)
> - ต้องการ Zero Maintenance — ไม่ต้อง manage server
> - ต้องการ Cost ต่ำ เพราะจ่ายเฉพาะเมื่อมี request
> - งานเป็น Short-lived tasks ไม่เกิน 15 นาที
>
> **เลือก EC2 + Flask เมื่อ:**
> - มี Long-running processes เช่น Background jobs, ML inference
> - มี Existing code/dependencies ที่ยากจะ port ไป Serverless
> - Traffic สูงสม่ำเสมอ — EC2 อาจถูกกว่า Lambda ในกรณีนี้
> - ต้องการ State ในหน่วยความจำระหว่าง requests
>
> **สำหรับ Student Record System**: Lambda เหมาะกว่า เพราะ Traffic น้อย ไม่ต่อเนื่อง และต้องการ Maintenance ต่ำ

---

**ข้อที่ 2. Defense in Depth — Security Layers**

> **เฉลย:** ระบบนี้มีความปลอดภัยแบบ Layered ดังนี้:
>
> **Layer 1 — Network**: Security Groups จำกัด Port และ Source IP ที่เข้าถึงแต่ละ Service ได้
>
> **Layer 2 — Access Control**: IAM Roles กำหนดว่า Lambda/EC2 จะเข้าถึง AWS Services ใดได้บ้าง (Least Privilege)
>
> **Layer 3 — Authentication**: API Key บน API Gateway ป้องกัน Unauthorized API Access
>
> **Layer 4 — Data in Transit**: HTTPS บน API Gateway เข้ารหัส Traffic ระหว่าง Client และ API
>
> **Layer 5 — Secrets Management**: SSM Parameter Store เก็บ DB Credentials แทนการ Hardcode
>
> **Layer 6 — Database**: RDS ไม่มี Public Access เข้าถึงได้เฉพาะจากภายใน VPC
>
> **Layer 7 — Application**: Parameterized Query ป้องกัน SQL Injection ใน Code

---

**ข้อที่ 3. Scalability Bottleneck**

> **เฉลย:** จาก Architecture ปัจจุบัน ถ้าผู้ใช้เพิ่มจาก 10 เป็น 10,000 คน:
>
> **Bottleneck ที่ 1 — RDS Connection (เกิดก่อน):**
> db.t3.micro มี max_connections ประมาณ 66 connections — 10,000 users พร้อมกันจะทำให้ Connection หมดทันที
>
> **วิธีแก้**: เพิ่ม Instance Size, ใช้ **RDS Proxy** ซึ่งทำ Connection Pooling ให้อัตโนมัติ
>
> **Bottleneck ที่ 2 — EC2 Single Instance:**
> EC2 t2.micro รับ Concurrent Connections ได้จำกัด
>
> **วิธีแก้**: ใช้ **Auto Scaling Group** + **Application Load Balancer**
>
> **Lambda** Scale ได้อัตโนมัติ จึงไม่เป็น Bottleneck (ยกเว้นถึง Account Concurrency Limit)

---

**ข้อที่ 4. RTO และ RPO**

> **เฉลย:**
> - **RTO (Recovery Time Objective)** = ระยะเวลาสูงสุดที่ระบบ Downtime ได้ก่อน Business ได้รับผลกระทบ
> - **RPO (Recovery Point Objective)** = ข้อมูลมากที่สุดที่ยอม "หาย" ได้ วัดเป็นระยะเวลาย้อนหลัง
>
> **สถานะปัจจุบัน (Single-AZ):**
> - RTO: ~10–30 นาที (ต้อง Restore RDS จาก Snapshot ด้วย Manual)
> - RPO: สูงสุด 24 ชั่วโมง (Automated Backup รายวัน) หรือเท่ากับ Transaction Log interval
>
> **ปรับปรุงได้โดย:**
> - เปิด **Multi-AZ**: RTO ลดเหลือ ~1–2 นาที (Automatic Failover)
> - เปิด **Enhanced Backups + Transaction Logs**: RPO ลดเหลือ ~5 นาที
> - ใช้ **Route 53 Health Checks**: Detect และ Failover อัตโนมัติ

---

**ข้อที่ 5. Cost Optimization**

> **เฉลย:** วิธีลดค่าใช้จ่าย AWS สำหรับระบบนี้:
>
> 1. **Reserved Instances**: ซื้อ EC2/RDS แบบ 1-year หรือ 3-year Reserved ลดได้ถึง **40–60%** เหมาะถ้าใช้ต่อเนื่อง
>
> 2. **Spot Instances (EC2)**: ใช้ Spot Instance สำหรับ Non-critical workloads ลดได้ถึง **70–90%** แต่ Instance อาจถูก Terminate ได้
>
> 3. **Graviton (ARM)**: เปลี่ยน EC2 เป็น t4g.micro (ARM-based) ราคาถูกกว่า t3.micro ประมาณ **20%** Performance ดีกว่าด้วย
>
> 4. **Lambda Architecture**: ย้าย EC2 Flask ไปเป็น Lambda ทั้งหมด ไม่ต้องจ่าย EC2 ตลอด 24 ชม.
>
> 5. **RDS Serverless v2**: ใช้ Aurora Serverless v2 แทน RDS — Scale ลงได้ถึง 0 ACU เมื่อไม่มีการใช้งาน ประหยัดในช่วง Low Traffic
>
> 6. **CloudFront**: นำ CloudFront มา Cache Static Content ลด Origin requests และ Data Transfer cost

---

---

## 📊 สรุปเกณฑ์การให้คะแนนแบบฝึกหัด

| สัปดาห์ | แบบฝึกหัด | คะแนนเต็ม | เกณฑ์ |
|---|---|---|---|
| **Week 1** | แบบฝึกหัดที่ 1 (PUT/DELETE) | 10 | โค้ดถูกต้อง 5, ทดสอบ Edge Case 3, Code Quality 2 |
| **Week 1** | แบบฝึกหัดที่ 2 (Monitoring) | 5 | บันทึกค่า Metrics 3, อธิบาย 2 |
| **Week 1** | คำถามท้ายบท (5 ข้อ) | 10 | ข้อละ 2 คะแนน |
| **Week 2** | แบบฝึกหัดที่ 1 (Enrollment) | 10 | POST 4, GET ทั้งสอง Endpoint 4, Error Handling 2 |
| **Week 2** | แบบฝึกหัดที่ 2 (Snapshot) | 5 | สร้าง Snapshot 3, บันทึก Details 2 |
| **Week 2** | คำถามท้ายบท (5 ข้อ) | 10 | ข้อละ 2 คะแนน |
| **Week 3** | แบบฝึกหัดที่ 1 (Search Lambda) | 10 | Function ทำงานได้ 5, Validation 3, API Gateway 2 |
| **Week 3** | แบบฝึกหัดที่ 2 (Throttling) | 5 | ตั้งค่าถูก 2, อธิบาย 3 |
| **Week 3** | คำถามท้ายบท (5 ข้อ) | 10 | ข้อละ 2 คะแนน |
| **Week 4** | แบบฝึกหัดที่ 1 (API Key) | 10 | ตั้งค่าครบ 5, ทดสอบ 3, อธิบายข้อจำกัด 2 |
| **Week 4** | แบบฝึกหัดที่ 2 (Logs Insights) | 5 | รัน Query ได้ 3, อ่านผลได้ถูกต้อง 2 |
| **Week 4** | คำถามท้ายบท (5 ข้อ) | 10 | ข้อละ 2 คะแนน |
| **รวม** | | **100** | |

---

*เอกสารเฉลยนี้จัดทำสำหรับ **อาจารย์อำนาจ คงเจริญถิ่น***  
*วิชา ICT 24267 Cloud Computing | ภาคการศึกษา 2/2568*
