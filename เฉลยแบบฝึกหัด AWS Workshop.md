# 📚 สรุปและเฉลย Quiz Preparation: ICT 24267 Cloud Computing
**อาจารย์อำนาจ คงเจริญถิ่น · ภาคการศึกษา 2/2568 · AWS Free Tier Workshop Week 1–4**

---

## 📅 Week 1: EC2 Advanced — Web Server & Flask
สร้าง Virtual Machine บน Cloud พร้อม Python Flask REST API และ Nginx Reverse Proxy
*(Tags: EC2 t3.micro, Amazon Linux 2023, Python Flask, Nginx, Security Groups, Elastic IP, User Data Script)*

### 📋 สรุป Key Concepts — Week 1
* ✅ **EC2 (Elastic Compute Cloud):** Virtual Machine บน AWS, เลือก type/OS/size ได้, จ่ายตามชั่วโมงที่ใช้
* ✅ **Key Pair (RSA):** กุญแจ SSH เข้า EC2 — `.pem` (Linux/Mac), `.ppk` (Windows+PuTTY), ดาวน์โหลดได้ครั้งเดียว
* ✅ **Security Group:** Virtual Firewall ควบคุม Inbound/Outbound traffic ระดับ Instance
* ✅ **User Data Script:** Script รันอัตโนมัติตอน Instance เปิดครั้งแรก ใช้ติดตั้ง software
* ✅ **Python Flask:** Web Framework เบาๆ สร้าง REST API — `@app.route()`, `jsonify()`, `request.get_json()`
* ✅ **Nginx Reverse Proxy:** รับ request Port 80 แล้วส่งต่อให้ Flask Port 5000 — ปลอดภัยและเสถียรกว่า
* ✅ **Elastic IP:** IP ถาวรที่ไม่เปลี่ยนเมื่อ Stop/Start — ฟรีเฉพาะตอน Instance กำลัง Running
* ✅ **systemd Service:** ทำให้ Flask รันอัตโนมัติเมื่อ reboot ด้วย `systemctl enable/start`

**Ports ที่ต้องจำ:**
| Port | Protocol | ใช้ทำอะไร | ใน Security Group |
|---|---|---|---|
| **22** | SSH | เข้าถึง EC2 ผ่าน Terminal | Inbound |
| **80** | HTTP | เว็บผ่าน Nginx | Inbound |
| **5000** | Custom TCP | Flask development server | Inbound |
| **3306** | MySQL | เชื่อมต่อ RDS (Week 2) | Inbound (RDS SG เท่านั้น) |

### ✏️ เฉลยแบบฝึกหัด Week 1
**1. เพิ่ม Endpoint PUT และ DELETE**
```python
# แบบฝึกหัดที่ 1 — PUT และ DELETE สำหรับ In-Memory list

@app.route('/students/<int:student_id>', methods=['PUT'])
def update_student(student_id):
    data = request.get_json()
    # หา student ใน list ด้วย next()
    student = next((s for s in students if s["id"] == student_id), None)
    if not student:
        return jsonify({"status": "error", "message": "Student not found"}), 404
    # อัปเดตเฉพาะ field ที่ส่งมา
    if "name" in data:
        student["name"] = data["name"]
    if "gpa" in data:
        student["gpa"] = data["gpa"]
    return jsonify({"status": "success", "data": student})

@app.route('/students/<int:student_id>', methods=['DELETE'])
def delete_student(student_id):
    global students
    original_len = len(students)
    students = [s for s in students if s["id"] != student_id]
    if len(students) == original_len:
        return jsonify({"status": "error", "message": "Student not found"}), 404
    return jsonify({"status": "success", "message": f"Student {student_id} deleted"})
