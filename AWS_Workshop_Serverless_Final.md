# 📅 WEEK 3–4: Serverless Computing บน AWS
## Mini Project: "ICT Feedback System" — ระบบรับ Feedback นักศึกษา

---

## 📑 สารบัญ Week 3–4

### Week 3 — รู้จัก Serverless และสร้าง API แรก
- [ทำความเข้าใจ Serverless คืออะไร](#-serverless-คืออะไร-อ่านก่อนลงมือ)
- [ภาพรวม Mini Project](#-ภาพรวม-mini-project-ict-feedback-system)
- [LAB 3-1: สร้าง DynamoDB Table (ฐานข้อมูล Serverless)](#-lab-3-1-สร้าง-dynamodb-table)
- [LAB 3-2: สร้าง IAM Role ให้ Lambda](#-lab-3-2-สร้าง-iam-role-ให้-lambda)
- [LAB 3-3: Lambda Function แรก — บันทึก Feedback](#-lab-3-3-lambda-function-แรก--บันทึก-feedback)
- [LAB 3-4: Lambda Function ที่สอง — ดึง Feedback](#-lab-3-4-lambda-function-ที่สอง--ดึง-feedback)
- [LAB 3-5: เปิด API ด้วย Function URL (ไม่ต้องใช้ API Gateway)](#-lab-3-5-เปิด-api-ด้วย-function-url)
- [LAB 3-6: ทดสอบ API ครั้งแรก](#-lab-3-6-ทดสอบ-api-ครั้งแรก)
- [แบบฝึกหัด Week 3](#-แบบฝึกหัด-week-3)
- [คำถามท้ายบท Week 3](#-คำถามท้ายบท-week-3)

### Week 4 — เพิ่ม Automation และ Monitoring
- [ภาพรวม Week 4](#-ภาพรวม-week-4)
- [LAB 4-1: Lambda Function ที่สาม — สรุปสถิติอัตโนมัติ (Scheduled)](#-lab-4-1-lambda-สรุปสถิติ--scheduled-trigger)
- [LAB 4-2: SNS — ส่ง Email แจ้งเตือนเมื่อมี Feedback ใหม่](#-lab-4-2-sns--ส่ง-email-แจ้งเตือนอัตโนมัติ)
- [LAB 4-3: CloudWatch — ดูสุขภาพระบบ](#-lab-4-3-cloudwatch--ดูสุขภาพระบบ)
- [LAB 4-4: สร้างหน้าเว็บ Frontend แบบง่าย](#-lab-4-4-frontend--หน้าเว็บสำหรับส่ง-feedback)
- [LAB 4-5: Cleanup — ลบ Resources หลัง LAB](#-lab-4-5-cleanup)
- [แบบฝึกหัด Week 4](#-แบบฝึกหัด-week-4)
- [คำถามท้ายบท Week 4](#-คำถามท้ายบท-week-4)
- [สรุปสิ่งที่เรียนรู้ตลอด 4 สัปดาห์](#-สรุปสิ่งที่เรียนรู้ตลอด-4-สัปดาห์)

---

---

# 📅 WEEK 3: รู้จัก Serverless และสร้าง API แรก

## 💡 Serverless คืออะไร? (อ่านก่อนลงมือ)

ก่อนเริ่ม LAB ขอให้ทำความเข้าใจ concept นี้ให้ชัดเจนก่อนครับ

### เปรียบเทียบแบบเข้าใจง่าย

| | แบบเดิม (EC2) | แบบ Serverless (Lambda) |
|---|---|---|
| **เปรียบเหมือน** | เช่าบ้านรายเดือน | จ้างแม่บ้านรายครั้ง |
| **จ่ายเงิน** | จ่ายตลอด 24 ชั่วโมง แม้ไม่มีคนใช้ | จ่ายเฉพาะตอนมีคนใช้จริง |
| **ดูแล Server** | ต้องดูแลเอง (update, security, restart) | AWS ดูแลให้ทั้งหมด |
| **รองรับคนใช้มาก** | ต้องวางแผนล่วงหน้า | ขยายตัวอัตโนมัติ |
| **เหมาะกับ** | งานที่รันต่อเนื่อง | งานที่รันตาม event |

### Serverless ทำงานอย่างไร?

```
ปกติ (ไม่มีคนใช้):   Lambda "หลับ" อยู่ → ไม่เสียเงิน

มีคนส่ง Feedback:
  1. HTTP Request เข้ามา
  2. Lambda "ตื่น" ใน ~100ms
  3. รันโค้ด บันทึกข้อมูล
  4. ส่งผลลัพธ์กลับ
  5. Lambda "หลับ" อีกครั้ง → ไม่เสียเงินต่อ
```

> 🎯 **สรุป**: Serverless = เราเขียนแค่ "โค้ดที่ต้องการ" AWS จัดการ Server ให้ทั้งหมด

### Services ที่ใช้ใน Week 3–4

```
┌─────────────────────────────────────────────────────┐
│                  AWS Free Tier Services              │
│                                                     │
│  Lambda    → รันโค้ด (1,000,000 ครั้ง/เดือน ฟรี)  │
│  DynamoDB  → เก็บข้อมูล (25 GB ฟรีตลอดไป)         │
│  SNS       → ส่ง Email แจ้งเตือน (1,000 ฟรี/เดือน)│
│  CloudWatch→ ดู Log และ Monitor (ฟรี basic)         │
└─────────────────────────────────────────────────────┘
```

---

## 🎯 ภาพรวม Mini Project: ICT Feedback System

เราจะสร้าง **ระบบรับ Feedback จากนักศึกษา** แบบ Serverless ทั้งหมด

### ระบบทำอะไรได้บ้าง?
1. **ส่ง Feedback** — นักศึกษาส่ง feedback พร้อมคะแนนความพึงพอใจ
2. **ดู Feedback ทั้งหมด** — ดึงรายการ feedback ย้อนหลังได้
3. **สรุปสถิติอัตโนมัติ** — คำนวณคะแนนเฉลี่ยทุกวัน
4. **แจ้งเตือนทาง Email** — เมื่อมี feedback ใหม่เข้ามา

### Architecture ของระบบ

```
นักศึกษา
    │  ส่ง Feedback (HTTP POST)
    ▼
┌─────────────────┐
│  Function URL   │  ← URL สาธารณะของ Lambda (ไม่ต้องใช้ API Gateway)
└────────┬────────┘
         │
    ┌────▼─────────────────────────────────────┐
    │         AWS Lambda Functions              │
    │                                          │
    │  📝 submit-feedback  → บันทึก Feedback   │
    │  📋 get-feedbacks    → ดึงข้อมูล         │
    │  📊 daily-summary    → สรุปรายวัน (Auto) │
    └────┬─────────────────────┬───────────────┘
         │                     │
    ┌────▼──────┐         ┌────▼──────┐
    │ DynamoDB  │         │    SNS    │
    │ (เก็บข้อมูล)│        │ (ส่ง Email)│
    └───────────┘         └───────────┘
         │
    ┌────▼──────┐
    │CloudWatch │
    │ (Log/Monitor)│
    └───────────┘
```

### ข้อมูล Feedback ที่เก็บ

| Field | ความหมาย | ตัวอย่าง |
|---|---|---|
| `feedback_id` | รหัส unique ของ feedback | `fb_1234567890` |
| `student_name` | ชื่อนักศึกษา | `สมชาย ใจดี` |
| `course` | รหัสวิชา | `ICT24267` |
| `rating` | คะแนน 1–5 | `5` |
| `comment` | ความคิดเห็น | `สอนดีมาก เข้าใจง่าย` |
| `timestamp` | เวลาที่ส่ง | `2026-03-19T10:30:00` |

---

## 🔧 LAB 3-1: สร้าง DynamoDB Table

### DynamoDB คืออะไร?

DynamoDB คือฐานข้อมูลแบบ **NoSQL** ของ AWS ที่ออกแบบมาสำหรับ Serverless โดยเฉพาะ

> 💡 **ต่างจาก MySQL ใน Week 2 อย่างไร?**
> - MySQL (RDS): ต้องมี Server รัน 24 ชั่วโมง, ข้อมูลเป็นตาราง
> - DynamoDB: ไม่มี Server, ข้อมูลเป็น key-value, **ฟรีตลอดไป** (25 GB)

### ขั้นตอนสร้าง Table

**1.** AWS Console → ค้นหา **DynamoDB** → คลิก **DynamoDB**

**2.** คลิกปุ่ม **Create table** (สีส้ม)

**3.** กรอกข้อมูล:

| ช่อง | ค่าที่ต้องกรอก |
|---|---|
| Table name | `ict24267-feedbacks` |
| Partition key | `feedback_id` |
| Partition key type | **String** |

**4.** ส่วน **Table settings** → เลือก **Customize settings**

**5.** ส่วน **Read/write capacity settings**:
   - เลือก **On-demand**
   > ✅ On-demand = จ่ายตามใช้จริง เหมาะกับ Free Tier ที่ traffic น้อย

**6.** ส่วนอื่นๆ ใช้ค่า default ทั้งหมด → คลิก **Create table**

**7.** รอสักครู่จนสถานะเปลี่ยนเป็น **Active** ✅

---

## 🔧 LAB 3-2: สร้าง IAM Role ให้ Lambda

Lambda ต้องมี "ใบอนุญาต" ก่อนจึงจะเข้าถึง DynamoDB และ SNS ได้

**1.** AWS Console → ค้นหา **IAM** → **Roles** → **Create role**

**2.** Trusted entity: **AWS service** → Use case: **Lambda** → **Next**

**3.** ค้นหาและเพิ่ม **3 Policies** นี้:

| ค้นหา | เลือก Policy | Lambda ทำอะไรได้ |
|---|---|---|
| `DynamoDBFull` | `AmazonDynamoDBFullAccess` | อ่าน/เขียน DynamoDB ได้ |
| `LambdaBasic` | `AWSLambdaBasicExecutionRole` | เขียน Log ได้ |
| `SNSFull` | `AmazonSNSFullAccess` | ส่ง Email ผ่าน SNS ได้ |

> ⚠️ ในงานจริง ควรจำกัด permission ให้แคบที่สุด แต่ในการเรียนใช้ FullAccess เพื่อความสะดวก

**4.** Role name: `ict24267-serverless-role` → **Create role**

---

## 🔧 LAB 3-3: Lambda Function แรก — บันทึก Feedback

Function นี้จะรับ Feedback จากนักศึกษาแล้วบันทึกลง DynamoDB

### ขั้นตอนที่ 1: สร้าง Function

**1.** AWS Console → **Lambda** → **Create function**

**2.** กรอกข้อมูล:
   - Function name: `ict24267-submit-feedback`
   - Runtime: **Python 3.11**
   - Architecture: **x86_64**

**3.** Permissions → **Change default execution role** → **Use an existing role** → `ict24267-serverless-role`

**4.** คลิก **Create function**

### ขั้นตอนที่ 2: วาง Code

คลิกที่ไฟล์ `lambda_function.py` → **ลบทั้งหมด** → **วาง code นี้**:

```python
import json
import boto3
import uuid
from datetime import datetime

# สร้าง DynamoDB client
dynamodb = boto3.resource('dynamodb', region_name='ap-southeast-1')
table = dynamodb.Table('ict24267-feedbacks')

def lambda_handler(event, context):
    """
    รับ Feedback จากนักศึกษาแล้วบันทึกลง DynamoDB
    
    รับข้อมูล JSON:
    {
        "student_name": "สมชาย ใจดี",
        "course": "ICT24267",
        "rating": 5,
        "comment": "สอนดีมาก"
    }
    """

    # --- Handle CORS preflight (browser จะส่ง OPTIONS มาก่อนเสมอ) ---
    if event.get('requestContext', {}).get('http', {}).get('method') == 'OPTIONS':
        return cors_response(200, {})

    try:
        # แปลง JSON string เป็น dictionary
        if isinstance(event.get('body'), str):
            body = json.loads(event['body'])
        else:
            body = event.get('body', {})

        # ตรวจสอบ field ที่จำเป็น
        required = ['student_name', 'course', 'rating']
        for field in required:
            if not body.get(field):
                return cors_response(400, {
                    'status': 'error',
                    'message': f'กรุณากรอก {field}'
                })

        # ตรวจสอบว่า rating อยู่ระหว่าง 1-5
        rating = int(body['rating'])
        if rating < 1 or rating > 5:
            return cors_response(400, {
                'status': 'error',
                'message': 'rating ต้องอยู่ระหว่าง 1-5'
            })

        # สร้าง feedback_id แบบ unique
        feedback_id = f"fb_{uuid.uuid4().hex[:10]}"

        # บันทึกลง DynamoDB
        item = {
            'feedback_id': feedback_id,
            'student_name': body['student_name'],
            'course': body['course'],
            'rating': rating,
            'comment': body.get('comment', ''),
            'timestamp': datetime.now().isoformat()
        }
        table.put_item(Item=item)

        # ส่งผลลัพธ์กลับ
        return cors_response(201, {
            'status': 'success',
            'message': 'บันทึก Feedback แล้ว ขอบคุณ! 🎉',
            'feedback_id': feedback_id
        })

    except Exception as e:
        return cors_response(500, {
            'status': 'error',
            'message': f'เกิดข้อผิดพลาด: {str(e)}'
        })


def cors_response(status_code, body):
    """สร้าง Response พร้อม CORS headers เพื่อให้ browser เรียกได้"""
    return {
        'statusCode': status_code,
        'headers': {
            'Content-Type': 'application/json; charset=utf-8',
            'Access-Control-Allow-Origin': '*',
            'Access-Control-Allow-Methods': 'GET,POST,OPTIONS',
            'Access-Control-Allow-Headers': 'Content-Type'
        },
        'body': json.dumps(body, ensure_ascii=False)
    }
```

**3.** คลิก **Deploy** (ปุ่มสีส้ม)

### ขั้นตอนที่ 3: ทดสอบ Function เบื้องต้น

**1.** แท็บ **Test** → **Create new event**

**2.** Event name: `test-submit` → แทนที่ JSON ทั้งหมดด้วย:

```json
{
  "body": "{\"student_name\": \"สมชาย ใจดี\", \"course\": \"ICT24267\", \"rating\": 5, \"comment\": \"สอนดีมากครับ เข้าใจง่าย\"}"
}
```

**3.** คลิก **Test**

**4.** ✅ ควรเห็น `"status": "success"` และ `"feedback_id": "fb_..."`

**5.** ไปตรวจสอบใน DynamoDB:
   - DynamoDB → **Tables** → `ict24267-feedbacks` → **Explore table items**
   - ✅ ควรเห็น item ที่เพิ่งบันทึก

---

## 🔧 LAB 3-4: Lambda Function ที่สอง — ดึง Feedback

Function นี้จะดึง feedback ทั้งหมดจาก DynamoDB ส่งกลับมา

### ขั้นตอนที่ 1: สร้าง Function

**1.** Lambda → **Create function**
   - Function name: `ict24267-get-feedbacks`
   - Runtime: **Python 3.11**
   - Execution role: `ict24267-serverless-role`

**2.** คลิก **Create function**

### ขั้นตอนที่ 2: วาง Code

**ลบทั้งหมด** → **วาง code นี้**:

```python
import json
import boto3
from boto3.dynamodb.conditions import Attr

# สร้าง DynamoDB client
dynamodb = boto3.resource('dynamodb', region_name='ap-southeast-1')
table = dynamodb.Table('ict24267-feedbacks')

def lambda_handler(event, context):
    """
    ดึง Feedback ทั้งหมดจาก DynamoDB
    
    รองรับ query parameters:
    - ?course=ICT24267  → กรองตามวิชา
    - ?rating=5         → กรองตาม rating
    """

    # Handle CORS
    if event.get('requestContext', {}).get('http', {}).get('method') == 'OPTIONS':
        return cors_response(200, {})

    try:
        # ดึง query parameters (ถ้ามี)
        params = event.get('queryStringParameters') or {}
        course = params.get('course')
        rating = params.get('rating')

        # ดึงข้อมูลจาก DynamoDB
        if course or rating:
            # กรองข้อมูล
            filter_expr = None

            if course:
                filter_expr = Attr('course').eq(course)
            if rating:
                rating_filter = Attr('rating').eq(int(rating))
                filter_expr = filter_expr & rating_filter if filter_expr else rating_filter

            response = table.scan(FilterExpression=filter_expr)
        else:
            # ดึงทั้งหมด
            response = table.scan()

        feedbacks = response.get('Items', [])

        # เรียงตามเวลา (ใหม่สุดก่อน)
        feedbacks.sort(key=lambda x: x.get('timestamp', ''), reverse=True)

        # คำนวณ rating เฉลี่ย
        avg_rating = 0
        if feedbacks:
            avg_rating = round(sum(int(f.get('rating', 0)) for f in feedbacks) / len(feedbacks), 2)

        return cors_response(200, {
            'status': 'success',
            'count': len(feedbacks),
            'average_rating': avg_rating,
            'data': feedbacks
        })

    except Exception as e:
        return cors_response(500, {
            'status': 'error',
            'message': f'เกิดข้อผิดพลาด: {str(e)}'
        })


def cors_response(status_code, body):
    return {
        'statusCode': status_code,
        'headers': {
            'Content-Type': 'application/json; charset=utf-8',
            'Access-Control-Allow-Origin': '*',
            'Access-Control-Allow-Methods': 'GET,POST,OPTIONS',
            'Access-Control-Allow-Headers': 'Content-Type'
        },
        'body': json.dumps(body, ensure_ascii=False, default=str)
    }
```

**3.** คลิก **Deploy**

### ขั้นตอนที่ 3: ทดสอบ

**1.** แท็บ **Test** → **Create new event** ชื่อ `test-get`

```json
{
  "queryStringParameters": null
}
```

**2.** คลิก **Test** → ✅ ควรเห็น feedback ที่บันทึกไว้ใน LAB 3-3

---

## 🔧 LAB 3-5: เปิด API ด้วย Function URL

ปกติ Lambda ไม่มี URL สาธารณะ เราต้องสร้าง **Function URL** เพื่อให้เรียกผ่าน Internet ได้

> 💡 **Function URL vs API Gateway**: Function URL ง่ายกว่า เหมาะกับ project เล็กๆ API Gateway ยืดหยุ่นกว่า เหมาะกับ production ขนาดใหญ่

### ทำกับ Function `ict24267-submit-feedback`

**1.** เปิด Lambda Function `ict24267-submit-feedback`

**2.** แท็บ **Configuration** → เมนูซ้าย **Function URL** → **Create function URL**

**3.** ตั้งค่า:
   - Auth type: **NONE** (เปิดให้ทุกคนเรียกได้ — เหมาะสำหรับการเรียน)
   - ✅ ติ๊ก **Configure cross-origin resource sharing (CORS)**

**4.** คลิก **Save**

**5.** ✅ **บันทึก Function URL** ที่ได้ เช่น:
   `https://abcdefgh.lambda-url.ap-southeast-1.on.aws/`

### ทำซ้ำกับ Function `ict24267-get-feedbacks`

ทำขั้นตอนเดิมทั้งหมดกับ Function `ict24267-get-feedbacks` → บันทึก URL นี้ด้วย

---

## 🔧 LAB 3-6: ทดสอบ API ครั้งแรก

ตอนนี้เรามี API ที่ทำงานได้จริงบน Internet แล้ว!

### ทดสอบผ่าน Browser (GET)

วาง URL ของ `ict24267-get-feedbacks` ใน browser โดยตรง เช่น:
```
https://xxxxxxxx.lambda-url.ap-southeast-1.on.aws/
```
✅ ควรเห็น JSON รายการ feedback

### ทดสอบผ่าน curl (POST)

แทนที่ `YOUR_SUBMIT_URL` ด้วย Function URL ของ `ict24267-submit-feedback`:

```bash
# ส่ง feedback ใหม่
curl -X POST YOUR_SUBMIT_URL \
  -H "Content-Type: application/json" \
  -d '{
    "student_name": "สมหญิง รักเรียน",
    "course": "ICT24267",
    "rating": 4,
    "comment": "เนื้อหาครบถ้วน อยากให้มี lab เพิ่มอีกครับ"
  }'

# ดู feedback ทั้งหมด
curl YOUR_GET_URL

# กรองเฉพาะวิชา ICT24267
curl "YOUR_GET_URL?course=ICT24267"

# กรองเฉพาะ rating 5
curl "YOUR_GET_URL?rating=5"
```

### ทดสอบผ่าน AWS Console (ไม่ต้องใช้ curl)

**1.** Lambda → `ict24267-submit-feedback` → แท็บ **Test**

**2.** สร้าง test events หลายๆ อัน เพื่อเพิ่ม feedback ตัวอย่าง:

```json
{
  "body": "{\"student_name\": \"วิไล มีแววดี\", \"course\": \"ICT24267\", \"rating\": 3, \"comment\": \"ยากเกินไปหน่อย แต่อาจารย์สอนดี\"}"
}
```

```json
{
  "body": "{\"student_name\": \"ประสิทธิ์ เรียนเก่ง\", \"course\": \"ICT24267\", \"rating\": 5, \"comment\": \"ชอบมาก ได้ความรู้เยอะ\"}"
}
```

**3.** ไปดูใน DynamoDB → `ict24267-feedbacks` → **Explore table items** เพื่อยืนยันว่าข้อมูลเข้า

---

## 📝 แบบฝึกหัด Week 3

### แบบฝึกหัดที่ 1: เพิ่ม Validation

แก้ไข `ict24267-submit-feedback` ให้ตรวจสอบเพิ่มเติม:
- `student_name` ต้องมีความยาวอย่างน้อย 2 ตัวอักษร
- `comment` ถ้ากรอกมา ต้องมีความยาวไม่เกิน 500 ตัวอักษร

เพิ่ม code ตรงส่วน "ตรวจสอบ field ที่จำเป็น" แล้ว Deploy ใหม่

### แบบฝึกหัดที่ 2: ทดสอบ Error Cases

ทดสอบส่ง request ที่ผิดพลาดแล้วบันทึกผลลัพธ์:

| กรณีทดสอบ | ผลลัพธ์ที่คาดหวัง |
|---|---|
| ไม่ส่ง `student_name` | `status: error` + message บอกว่า field อะไรขาด |
| `rating` เป็น 6 | `status: error` + message บอก rating ไม่ถูกต้อง |
| `rating` เป็น "abc" | เกิด error อะไร? |

---

## 🗒️ คำถามท้ายบท Week 3

1. **Serverless vs Traditional**: จากที่ได้ทดลองใช้ทั้ง EC2 (Week 1-2) และ Lambda (Week 3) อธิบายว่า ถ้าระบบมีคนใช้งาน 1,000 คน/วัน แต่กระจุกตัวในช่วง 9:00-17:00 น. ควรใช้แบบไหน? เพราะอะไร?

2. **DynamoDB vs RDS**: เปรียบเทียบ DynamoDB (Week 3) กับ MySQL บน RDS (Week 2) ในแง่ของ: โครงสร้างข้อมูล, การ query ข้อมูล, ค่าใช้จ่าย และความเหมาะสมกับงานแต่ละประเภท

3. **Function URL vs API Gateway**: ในระบบ Feedback นี้เราใช้ Function URL แทน API Gateway เหมือน Workshop เดิม อธิบายข้อดีข้อเสียของแต่ละแบบ และสถานการณ์ใดควรใช้อะไร?

4. **Cold Start**: เมื่อกด Test ครั้งแรกหลังสร้าง Lambda ใหม่ มักใช้เวลานานกว่าครั้งถัดไป เรียกปรากฏการณ์นี้ว่า "Cold Start" — อธิบายว่าเกิดจากอะไร และมีผลกระทบอย่างไรต่อ User Experience?

5. **IAM Role**: ในขั้นตอน LAB 3-2 เราให้ `AmazonDynamoDBFullAccess` แก่ Lambda แต่จริงๆ แล้ว Function นี้ต้องการ permission อะไรบ้าง? การให้ permission เกินความจำเป็นมีความเสี่ยงอะไร?

---

---

# 📅 WEEK 4: Automation, Monitoring และ Frontend

## 🎯 ภาพรวม Week 4

สัปดาห์นี้จะ **เพิ่มความสามารถ** ให้ระบบ Feedback โดยไม่ต้องเขียน Server เพิ่มเลย

```
Week 3 (ที่ทำแล้ว):        Week 4 (จะเพิ่ม):
━━━━━━━━━━━━━━━━━━━━        ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
submit-feedback  ✅    →    + แจ้ง Email ทันทีเมื่อมี feedback ใหม่
get-feedbacks    ✅    →    + สรุปสถิติอัตโนมัติทุกเช้า
                            + หน้าเว็บสำหรับส่ง feedback
                            + Dashboard ดูสุขภาพระบบ
```

---

## 🔧 LAB 4-1: Lambda สรุปสถิติ + Scheduled Trigger

เราจะสร้าง Function ที่ **รันอัตโนมัติทุกวัน** เพื่อสรุปสถิติ feedback โดยไม่มีคนกด

> 💡 **Scheduled Trigger คืออะไร?** คือการตั้งเวลาให้ Lambda รันเองอัตโนมัติ เหมือน Cron Job แต่ไม่ต้องมี Server

### ขั้นตอนที่ 1: สร้าง Function

**1.** Lambda → **Create function**
   - Function name: `ict24267-daily-summary`
   - Runtime: **Python 3.11**
   - Execution role: `ict24267-serverless-role`

**2.** คลิก **Create function**

### ขั้นตอนที่ 2: วาง Code

**ลบทั้งหมด** → **วาง code นี้**:

```python
import json
import boto3
from datetime import datetime, date
from boto3.dynamodb.conditions import Attr
from decimal import Decimal

dynamodb = boto3.resource('dynamodb', region_name='ap-southeast-1')
table = dynamodb.Table('ict24267-feedbacks')

def lambda_handler(event, context):
    """
    สรุปสถิติ Feedback ประจำวัน
    รันอัตโนมัติทุกวันตอน 08:00 น. ไทย
    """
    print("🔄 เริ่มสรุปสถิติประจำวัน...")

    try:
        # ดึง feedback ทั้งหมด
        response = table.scan()
        all_feedbacks = response.get('Items', [])

        if not all_feedbacks:
            print("ℹ️ ยังไม่มี feedback")
            return {'statusCode': 200, 'body': 'ไม่มีข้อมูล feedback'}

        # คำนวณสถิติ
        total       = len(all_feedbacks)
        ratings     = [int(f.get('rating', 0)) for f in all_feedbacks]
        avg_rating  = round(sum(ratings) / total, 2)

        # นับตาม rating
        rating_dist = {str(i): ratings.count(i) for i in range(1, 6)}

        # นับตามวิชา
        course_dist = {}
        for f in all_feedbacks:
            course = f.get('course', 'ไม่ระบุ')
            course_dist[course] = course_dist.get(course, 0) + 1

        # feedback ล่าสุด 3 อัน
        sorted_feedbacks = sorted(all_feedbacks,
                                  key=lambda x: x.get('timestamp', ''),
                                  reverse=True)
        recent = [
            {
                'student': f.get('student_name'),
                'course':  f.get('course'),
                'rating':  int(f.get('rating', 0)),
                'comment': f.get('comment', '')[:50]  # ตัดให้สั้น
            }
            for f in sorted_feedbacks[:3]
        ]

        summary = {
            'report_date':   str(date.today()),
            'total_feedbacks': total,
            'average_rating':  avg_rating,
            'rating_distribution': rating_dist,
            'by_course':     course_dist,
            'recent_3':      recent
        }

        # แสดงใน CloudWatch Log
        print(f"📊 สรุปประจำวัน {summary['report_date']}:")
        print(f"   รวม feedback : {total} รายการ")
        print(f"   คะแนนเฉลี่ย  : {avg_rating} / 5")
        print(f"   แจกแจง rating: {rating_dist}")
        print(f"   แยกตามวิชา  : {course_dist}")
        print("✅ สรุปสถิติเสร็จแล้ว")

        return {
            'statusCode': 200,
            'body': json.dumps(summary, ensure_ascii=False, default=str)
        }

    except Exception as e:
        print(f"❌ Error: {str(e)}")
        raise
```

**3.** คลิก **Deploy**

### ขั้นตอนที่ 3: ทดสอบ Function ก่อน

**1.** แท็บ **Test** → **Create new event** ชื่อ `test-summary`

```json
{}
```

**2.** คลิก **Test** → ✅ ควรเห็นสถิติ feedback ที่มีอยู่

**3.** ดู **Log output** ด้านล่าง — จะเห็น print statements ที่เขียนไว้

### ขั้นตอนที่ 4: ตั้ง Schedule ให้รันทุกวันอัตโนมัติ

**1.** แท็บ **Configuration** → **Triggers** → **Add trigger**

**2.** ตั้งค่า:
   - Trigger source: **EventBridge (CloudWatch Events)**
   - Rule: **Create a new rule**
   - Rule name: `ict24267-daily-summary-schedule`
   - Rule type: **Schedule expression**
   - Schedule expression: `cron(0 1 * * ? *)`

   > 📅 **อ่านค่า cron**: `cron(นาที ชั่วโมง วัน เดือน วันอาทิตย์ ปี)`
   > `0 1 * * ? *` = ทุกวัน เวลา 01:00 UTC = **08:00 น. ไทย**

**3.** คลิก **Add**

✅ ตั้งแต่นี้ไป Function จะรันอัตโนมัติทุกเช้า 8 โมง โดยไม่มีคนกด

---

## 🔧 LAB 4-2: SNS — ส่ง Email แจ้งเตือนอัตโนมัติ

เราจะแก้ไข `ict24267-submit-feedback` ให้ **ส่ง Email แจ้งเตือนทันที** เมื่อมี feedback ใหม่

> 💡 **SNS (Simple Notification Service)** คือบริการส่งข้อความของ AWS รองรับ Email, SMS, และ Push Notification

### ขั้นตอนที่ 1: สร้าง SNS Topic

**1.** AWS Console → ค้นหา **SNS** → **Simple Notification Service**

**2.** เมนูซ้าย **Topics** → **Create topic**

**3.** ตั้งค่า:
   - Type: **Standard**
   - Name: `ict24267-feedback-alerts`

**4.** คลิก **Create topic**

**5.** ✅ **บันทึก Topic ARN** ที่ได้ เช่น:
   `arn:aws:sns:ap-southeast-1:123456789:ict24267-feedback-alerts`

### ขั้นตอนที่ 2: Subscribe Email ของคุณ

**1.** ในหน้า Topic → คลิก **Create subscription**

**2.** ตั้งค่า:
   - Protocol: **Email**
   - Endpoint: **ใส่ Email ของคุณ**

**3.** คลิก **Create subscription**

**4.** ✅ **ไปเช็ค Email** → คลิก **Confirm subscription** (ถ้าไม่ยืนยัน จะไม่ได้รับแจ้งเตือน)

### ขั้นตอนที่ 3: อัปเดต submit-feedback ให้ส่ง Email

**1.** Lambda → `ict24267-submit-feedback` → แท็บ **Code**

**2.** **ลบทั้งหมด** → **วาง code ใหม่นี้** (เพิ่ม SNS เข้าไป):

> ⚠️ แทนที่ `YOUR_SNS_TOPIC_ARN` ด้วย ARN จริงที่ได้จากขั้นตอนที่ 1

```python
import json
import boto3
import uuid
from datetime import datetime

dynamodb = boto3.resource('dynamodb', region_name='ap-southeast-1')
table    = dynamodb.Table('ict24267-feedbacks')

sns      = boto3.client('sns', region_name='ap-southeast-1')
# ⚠️ แทนที่ด้วย SNS Topic ARN จริงของคุณ
SNS_TOPIC_ARN = 'YOUR_SNS_TOPIC_ARN'

def lambda_handler(event, context):
    # Handle CORS preflight
    if event.get('requestContext', {}).get('http', {}).get('method') == 'OPTIONS':
        return cors_response(200, {})

    try:
        if isinstance(event.get('body'), str):
            body = json.loads(event['body'])
        else:
            body = event.get('body', {})

        # ตรวจสอบ field ที่จำเป็น
        required = ['student_name', 'course', 'rating']
        for field in required:
            if not body.get(field):
                return cors_response(400, {
                    'status': 'error',
                    'message': f'กรุณากรอก {field}'
                })

        rating = int(body['rating'])
        if rating < 1 or rating > 5:
            return cors_response(400, {
                'status': 'error',
                'message': 'rating ต้องอยู่ระหว่าง 1-5'
            })

        # สร้าง feedback_id และบันทึกลง DynamoDB
        feedback_id = f"fb_{uuid.uuid4().hex[:10]}"
        item = {
            'feedback_id':  feedback_id,
            'student_name': body['student_name'],
            'course':       body['course'],
            'rating':       rating,
            'comment':      body.get('comment', ''),
            'timestamp':    datetime.now().isoformat()
        }
        table.put_item(Item=item)

        # --- ส่ง Email แจ้งเตือนผ่าน SNS ---
        stars = '⭐' * rating
        email_message = f"""
มี Feedback ใหม่เข้ามา!
─────────────────────────────
นักศึกษา : {body['student_name']}
วิชา      : {body['course']}
คะแนน    : {stars} ({rating}/5)
ความคิดเห็น: {body.get('comment', '(ไม่มีความคิดเห็น)')}
เวลา      : {item['timestamp']}
Feedback ID: {feedback_id}
─────────────────────────────
        """.strip()

        sns.publish(
            TopicArn=SNS_TOPIC_ARN,
            Subject=f'[ICT24267] Feedback ใหม่จาก {body["student_name"]} - {stars}',
            Message=email_message
        )

        return cors_response(201, {
            'status':      'success',
            'message':     'บันทึก Feedback แล้ว ขอบคุณ! 🎉',
            'feedback_id': feedback_id
        })

    except Exception as e:
        return cors_response(500, {
            'status':  'error',
            'message': f'เกิดข้อผิดพลาด: {str(e)}'
        })


def cors_response(status_code, body):
    return {
        'statusCode': status_code,
        'headers': {
            'Content-Type': 'application/json; charset=utf-8',
            'Access-Control-Allow-Origin': '*',
            'Access-Control-Allow-Methods': 'GET,POST,OPTIONS',
            'Access-Control-Allow-Headers': 'Content-Type'
        },
        'body': json.dumps(body, ensure_ascii=False)
    }
```

**3.** คลิก **Deploy**

### ขั้นตอนที่ 4: ทดสอบ Email

**1.** แท็บ **Test** → รัน `test-submit` อีกครั้ง

**2.** ✅ ไปเช็ค Email — ควรได้รับแจ้งเตือนภายใน 1-2 นาที

---

## 🔧 LAB 4-3: CloudWatch — ดูสุขภาพระบบ

CloudWatch เก็บ Log ทุกครั้งที่ Lambda รัน ทำให้ debug และ monitor ได้

### ขั้นตอนที่ 1: ดู Log ของ Lambda

**1.** Lambda → เปิด Function ใดก็ได้ → แท็บ **Monitor**

**2.** คลิก **View CloudWatch logs**

**3.** คลิก Log stream ล่าสุด → จะเห็น log ทุก request

**4.** ✅ ค้นหา `print` statements ที่เราเขียนไว้ใน code

### ขั้นตอนที่ 2: สร้าง Dashboard เพื่อดูภาพรวม

**1.** AWS Console → **CloudWatch** → **Dashboards** → **Create dashboard**

**2.** Dashboard name: `ICT24267-Feedback-System` → **Create dashboard**

**3.** เพิ่ม Widget: **Add widget** → **Line** → **Next**
   - Metrics → **Lambda** → **By Function Name**
   - ติ๊กเลือก `Invocations` และ `Errors` ของทั้ง 3 Functions
   - คลิก **Create widget**

**4.** เพิ่ม Widget อีกอัน: **Add widget** → **Number** → **Next**
   - Metrics → **Lambda** → **By Function Name**
   - ติ๊กเลือก `Duration` (เวลาที่รัน)
   - คลิก **Create widget**

**5.** คลิก **Save dashboard**

### ขั้นตอนที่ 3: สร้าง Alarm แจ้งเตือนเมื่อ Lambda Error

**1.** CloudWatch → **Alarms** → **Create alarm** → **Select metric**

**2.** Lambda → By Function Name → `ict24267-submit-feedback` → `Errors` → **Select metric**

**3.** Condition:
   - Whenever Errors is: **Greater than or equal to**
   - than: `3`
   - Datapoints: `1 out of 5`

**4.** Notification: **Create new topic**
   - Topic name: `ict24267-system-alerts`
   - Email: ใส่ Email ของคุณ → **Create topic**

**5.** Alarm name: `ict24267-lambda-errors` → **Create alarm**

**6.** ✅ ยืนยัน Email subscription อีกครั้ง

---

## 🔧 LAB 4-4: Frontend — หน้าเว็บสำหรับส่ง Feedback

สร้างหน้าเว็บง่ายๆ สำหรับส่ง feedback โดยใช้ S3 Static Website Hosting (ฟรี)

> 💡 **S3 Static Website** คือการใช้ S3 bucket เก็บไฟล์ HTML แล้วเปิดเป็นเว็บได้เลย ไม่ต้องมี Server

### ขั้นตอนที่ 1: สร้าง S3 Bucket

**1.** AWS Console → **S3** → **Create bucket**

**2.** ตั้งค่า:
   - Bucket name: `ict24267-feedback-web-` + เลขนักศึกษาของคุณ เช่น `ict24267-feedback-web-6401001`
     > ✅ ชื่อ S3 bucket ต้อง unique ทั่วโลก ให้ใส่เลขนักศึกษาต่อท้าย
   - Region: **ap-southeast-1**
   - Block all public access: **ยกเลิกติ๊ก** (ต้องการให้เข้าถึงได้)
   - ✅ ติ๊ก "I acknowledge that the current settings might result in..."

**3.** คลิก **Create bucket**

### ขั้นตอนที่ 2: เปิด Static Website Hosting

**1.** เปิด bucket → แท็บ **Properties**

**2.** เลื่อนลงหา **Static website hosting** → **Edit**

**3.** ตั้งค่า:
   - Static website hosting: **Enable**
   - Index document: `index.html`

**4.** คลิก **Save changes**

### ขั้นตอนที่ 3: ตั้งค่า Bucket Policy

**1.** แท็บ **Permissions** → **Bucket policy** → **Edit**

**2.** วาง policy นี้ (แทนที่ `YOUR-BUCKET-NAME` ด้วยชื่อ bucket จริงของคุณ):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::YOUR-BUCKET-NAME/*"
    }
  ]
}
```

**3.** คลิก **Save changes**

### ขั้นตอนที่ 4: สร้างไฟล์ `index.html`

สร้างไฟล์ชื่อ `index.html` บนเครื่องตัวเอง แล้ว **วาง code ทั้งหมดนี้**:

> ⚠️ **แทนที่ 2 ค่านี้ก่อน upload:**
> - `YOUR_SUBMIT_URL` → Function URL ของ `ict24267-submit-feedback`
> - `YOUR_GET_URL` → Function URL ของ `ict24267-get-feedbacks`

```html
<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>ICT24267 — Feedback System</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(135deg, #1a1a2e 0%, #16213e 50%, #0f3460 100%);
      min-height: 100vh; padding: 20px; color: #e0e0e0;
    }
    .container { max-width: 800px; margin: 0 auto; }
    .header {
      text-align: center; padding: 30px 0 20px;
      border-bottom: 2px solid #e94560; margin-bottom: 24px;
    }
    .header h1 { font-size: 1.8em; color: #e94560; margin-bottom: 6px; }
    .header p  { color: #a0a0b0; font-size: 0.9em; }
    .card {
      background: rgba(255,255,255,0.05);
      border: 1px solid rgba(255,255,255,0.1);
      border-radius: 12px; padding: 24px; margin-bottom: 20px;
    }
    .card h2 { color: #e94560; margin-bottom: 16px; font-size: 1.1em; }
    .form-group { margin-bottom: 14px; }
    label { display: block; margin-bottom: 5px; font-size: 0.85em; color: #a0a0b0; }
    input, textarea, select {
      width: 100%; padding: 10px 12px;
      background: rgba(255,255,255,0.08); border: 1px solid rgba(255,255,255,0.15);
      border-radius: 8px; color: #e0e0e0; font-size: 0.9em;
    }
    textarea { height: 80px; resize: vertical; }
    .stars { display: flex; gap: 8px; margin-top: 5px; }
    .star {
      font-size: 1.8em; cursor: pointer; transition: transform 0.1s;
      filter: grayscale(1); opacity: 0.4;
    }
    .star.active { filter: none; opacity: 1; transform: scale(1.1); }
    .btn {
      width: 100%; padding: 12px; border: none; border-radius: 8px;
      font-size: 1em; font-weight: 700; cursor: pointer; transition: opacity 0.2s;
    }
    .btn-primary { background: #e94560; color: white; }
    .btn-secondary { background: rgba(255,255,255,0.1); color: #e0e0e0; margin-top: 10px; }
    .btn:hover { opacity: 0.85; }
    #msg {
      padding: 10px 14px; border-radius: 8px; margin-top: 12px;
      display: none; font-size: 0.9em; text-align: center;
    }
    .success { background: rgba(40,167,69,0.3); color: #7dffb3; border: 1px solid #28a745; }
    .error   { background: rgba(220,53,69,0.3);  color: #ffaaaa; border: 1px solid #dc3545; }
    .stat-row { display: flex; gap: 12px; margin-bottom: 16px; }
    .stat { flex: 1; background: rgba(233,69,96,0.15); border-radius: 8px;
            padding: 14px; text-align: center; }
    .stat-num   { font-size: 1.8em; font-weight: 700; color: #e94560; }
    .stat-label { font-size: 0.75em; color: #a0a0b0; margin-top: 3px; }
    .feedback-item {
      background: rgba(255,255,255,0.04); border-radius: 8px;
      padding: 12px; margin-bottom: 10px; border-left: 3px solid #e94560;
    }
    .feedback-meta { display: flex; justify-content: space-between;
                     font-size: 0.8em; color: #a0a0b0; margin-bottom: 5px; }
    .feedback-comment { font-size: 0.9em; }
    .feedback-stars { color: #ffd700; }
    .loading { text-align: center; color: #a0a0b0; padding: 20px; }
  </style>
</head>
<body>
<div class="container">
  <div class="header">
    <h1>🎓 ICT24267 Feedback System</h1>
    <p>Cloud Computing | ภาคการศึกษา 2/2568 | Powered by AWS Lambda + DynamoDB</p>
  </div>

  <!-- ฟอร์มส่ง Feedback -->
  <div class="card">
    <h2>📝 ส่ง Feedback</h2>
    <div class="form-group">
      <label>ชื่อ-นามสกุล *</label>
      <input type="text" id="name" placeholder="ชื่อภาษาไทยหรืออังกฤษ">
    </div>
    <div class="form-group">
      <label>รหัสวิชา *</label>
      <input type="text" id="course" value="ICT24267" placeholder="เช่น ICT24267">
    </div>
    <div class="form-group">
      <label>คะแนนความพึงพอใจ *</label>
      <div class="stars" id="stars">
        <span class="star" data-val="1">⭐</span>
        <span class="star" data-val="2">⭐</span>
        <span class="star" data-val="3">⭐</span>
        <span class="star" data-val="4">⭐</span>
        <span class="star" data-val="5">⭐</span>
      </div>
    </div>
    <div class="form-group">
      <label>ความคิดเห็น (ไม่บังคับ)</label>
      <textarea id="comment" placeholder="บอกเราว่าชอบหรือไม่ชอบอะไร..."></textarea>
    </div>
    <button class="btn btn-primary" onclick="submitFeedback()">ส่ง Feedback</button>
    <div id="msg"></div>
  </div>

  <!-- สถิติและรายการ Feedback -->
  <div class="card">
    <h2>📊 Feedback ทั้งหมด</h2>
    <div class="stat-row">
      <div class="stat"><div class="stat-num" id="totalCount">-</div><div class="stat-label">รายการทั้งหมด</div></div>
      <div class="stat"><div class="stat-num" id="avgRating">-</div><div class="stat-label">คะแนนเฉลี่ย / 5</div></div>
    </div>
    <button class="btn btn-secondary" onclick="loadFeedbacks()">🔄 โหลด Feedback</button>
    <div id="feedbackList" style="margin-top:16px">
      <div class="loading">กด "โหลด Feedback" เพื่อดูรายการ</div>
    </div>
  </div>
</div>

<script>
  // ⚠️ แทนที่ด้วย Function URL จริงของคุณ
  const SUBMIT_URL = 'YOUR_SUBMIT_URL';
  const GET_URL    = 'YOUR_GET_URL';

  let selectedRating = 0;

  // Star rating interaction
  document.querySelectorAll('.star').forEach(star => {
    star.addEventListener('click', () => {
      selectedRating = parseInt(star.dataset.val);
      document.querySelectorAll('.star').forEach((s, i) => {
        s.classList.toggle('active', i < selectedRating);
      });
    });
  });

  function showMsg(text, type) {
    const el = document.getElementById('msg');
    el.textContent = text; el.className = type; el.style.display = 'block';
    setTimeout(() => el.style.display = 'none', 4000);
  }

  async function submitFeedback() {
    const name    = document.getElementById('name').value.trim();
    const course  = document.getElementById('course').value.trim();
    const comment = document.getElementById('comment').value.trim();

    if (!name)          return showMsg('⚠️ กรุณากรอกชื่อ', 'error');
    if (!course)        return showMsg('⚠️ กรุณากรอกรหัสวิชา', 'error');
    if (!selectedRating)return showMsg('⚠️ กรุณาเลือกคะแนน', 'error');

    try {
      const res  = await fetch(SUBMIT_URL, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ student_name: name, course, rating: selectedRating, comment })
      });
      const data = await res.json();

      if (data.status === 'success') {
        showMsg('✅ ขอบคุณสำหรับ Feedback!', 'success');
        document.getElementById('name').value    = '';
        document.getElementById('comment').value = '';
        selectedRating = 0;
        document.querySelectorAll('.star').forEach(s => s.classList.remove('active'));
        loadFeedbacks();
      } else {
        showMsg('❌ ' + data.message, 'error');
      }
    } catch (e) {
      showMsg('❌ เชื่อมต่อไม่ได้: ' + e.message, 'error');
    }
  }

  async function loadFeedbacks() {
    const list = document.getElementById('feedbackList');
    list.innerHTML = '<div class="loading">⏳ กำลังโหลด...</div>';
    try {
      const res  = await fetch(GET_URL);
      const data = await res.json();
      const items = data.data || [];

      document.getElementById('totalCount').textContent = data.count || 0;
      document.getElementById('avgRating').textContent  = data.average_rating || '-';

      if (items.length === 0) {
        list.innerHTML = '<div class="loading">ยังไม่มี Feedback</div>';
        return;
      }
      list.innerHTML = items.map(f => `
        <div class="feedback-item">
          <div class="feedback-meta">
            <span>👤 ${f.student_name} — ${f.course}</span>
            <span>${(f.timestamp||'').substring(0,10)}</span>
          </div>
          <div class="feedback-stars">${'⭐'.repeat(parseInt(f.rating||0))}</div>
          ${f.comment ? `<div class="feedback-comment" style="margin-top:5px">${f.comment}</div>` : ''}
        </div>
      `).join('');
    } catch (e) {
      list.innerHTML = `<div class="loading" style="color:#ff8888">❌ โหลดไม่ได้: ${e.message}</div>`;
    }
  }
</script>
</body>
</html>
```

### ขั้นตอนที่ 5: Upload ไฟล์ขึ้น S3

**1.** S3 → เปิด bucket ของคุณ → คลิก **Upload**

**2.** **Add files** → เลือกไฟล์ `index.html` ที่เพิ่งสร้าง

**3.** คลิก **Upload**

### ขั้นตอนที่ 6: เปิดเว็บ

**1.** แท็บ **Properties** → เลื่อนลงหา **Static website hosting**

**2.** คลิก **Bucket website endpoint** URL เช่น:
   `http://ict24267-feedback-web-6401001.s3-website-ap-southeast-1.amazonaws.com`

**3.** ✅ ควรเห็นหน้า Feedback System พร้อมใช้งาน!

---

## 🔧 LAB 4-5: Cleanup

> ⚠️ ทำทุกขั้นตอนนี้หลัง LAB สิ้นสุด เพื่อไม่ให้เกิดค่าใช้จ่าย

### ลำดับการ Cleanup (ทำตามลำดับ)

```
1. EventBridge → Rules → ลบ ict24267-daily-summary-schedule
2. Lambda → ลบ Functions ทั้ง 3 ตัว
3. SNS → Subscriptions → ลบ subscription
      → Topics → ลบ ict24267-feedback-alerts
4. S3 → เปิด bucket → ลบไฟล์ทั้งหมด → ลบ bucket
5. DynamoDB → Tables → เลือก ict24267-feedbacks → Delete table
6. CloudWatch → Dashboards → ลบ ICT24267-Feedback-System
             → Alarms → ลบ Alarm ทั้งหมด
7. IAM → Roles → ลบ ict24267-serverless-role
```

> 💡 DynamoDB Always Free ไม่มีค่าใช้จ่ายแม้ไม่ลบ แต่ควรลบเพื่อความเป็นระเบียบ

---

## 📝 แบบฝึกหัด Week 4

### แบบฝึกหัดที่ 1: เพิ่ม Filter ใน Daily Summary

แก้ไข `ict24267-daily-summary` ให้สรุปเฉพาะ feedback ที่เข้ามาในวันนี้เท่านั้น (ไม่ใช่ทั้งหมดตั้งแต่ต้น)

**힌트**: ใช้ `FilterExpression` กับ `Attr('timestamp').begins_with(str(date.today()))`

### แบบฝึกหัดที่ 2: ปรับแต่ง Frontend

แก้ไขไฟล์ `index.html` ให้:
- เพิ่มช่อง dropdown สำหรับเลือกชื่ออาจารย์
- เพิ่มปุ่มกรองแสดงเฉพาะ feedback ที่ rating 5 ดาว
- เปลี่ยนสีธีมตามความชอบ

---

## 🗒️ คำถามท้ายบท Week 4

1. **Event-Driven Architecture**: ในระบบ Feedback นี้มี 2 แบบของ trigger: HTTP Request (คนกด) และ Schedule (รันเอง) อธิบายว่าแต่ละแบบเหมาะกับงานประเภทใด และยกตัวอย่าง use case จริงในโลก IT

2. **SNS vs SES**: AWS มีบริการส่ง Email 2 แบบ คือ SNS (Simple Notification Service) และ SES (Simple Email Service) — อธิบายความแตกต่าง และระบบ Feedback ของเราควรใช้แบบใดถ้าต้องการส่ง Email สวยงามมี HTML?

3. **S3 Static Website**: เปรียบเทียบการ host Frontend ด้วย S3 Static Website กับการ host บน EC2 + Nginx (Week 1) ในแง่ของ: ความยุ่งยาก, ค่าใช้จ่าย, และ Scalability

4. **Observability**: จาก CloudWatch Log ที่ดูใน LAB 4-3 อธิบายความแตกต่างระหว่าง Logging, Monitoring และ Alerting ทั้ง 3 อย่างนี้มีความสำคัญอย่างไรในระบบ Production?

5. **Architecture Review**: มองภาพรวมทั้ง 4 สัปดาห์ ระบบมี 2 ส่วนคือ EC2+RDS+Flask (Week 1-2) และ Lambda+DynamoDB (Week 3-4) — ถ้าต้องเลือกสร้างระบบใหม่ในอนาคต คุณจะเลือก Architecture แบบไหน? เพราะอะไร?

---

---

## 📚 สรุปสิ่งที่เรียนรู้ตลอด 4 สัปดาห์

```
Week 1 — EC2 + Flask
  ✅ สร้าง Virtual Machine บน Cloud
  ✅ Deploy Web Application ด้วย Python Flask
  ✅ ตั้งค่า Security Group, Elastic IP, Nginx

Week 2 — RDS + Database
  ✅ สร้างฐานข้อมูล MySQL บน Cloud (Managed Service)
  ✅ เชื่อมต่อ Application กับ Database อย่างปลอดภัย
  ✅ CRUD Operations ผ่าน API

Week 3 — Lambda + DynamoDB (Serverless)
  ✅ เข้าใจแนวคิด Serverless Architecture
  ✅ สร้าง Lambda Function แบบ Event-Driven
  ✅ ใช้ DynamoDB ฐานข้อมูล NoSQL แบบ Serverless
  ✅ เปิด API ด้วย Function URL

Week 4 — Automation + Monitoring + Frontend
  ✅ Scheduled Tasks ด้วย EventBridge
  ✅ Real-time Notification ด้วย SNS
  ✅ Monitoring ด้วย CloudWatch
  ✅ Static Website Hosting บน S3
```

### Serverless vs Traditional — สรุปสุดท้าย

| | EC2 + RDS (Traditional) | Lambda + DynamoDB (Serverless) |
|---|---|---|
| **เราดูแล** | OS, Runtime, Scaling, Availability | เฉพาะ Code เท่านั้น |
| **AWS ดูแล** | Hardware | Hardware + OS + Runtime + Scaling |
| **จ่ายเงิน** | ตลอด 24 ชั่วโมง | เฉพาะตอนรัน (ms) |
| **เริ่มต้น** | ซับซ้อนกว่า | ง่ายกว่า |
| **เหมาะกับ** | งาน stateful, real-time, ต่อเนื่อง | งาน event-driven, traffic ไม่แน่นอน |
| **ตัวอย่าง** | E-commerce, Game Server | Chatbot, Image Processing, API |

> 🎯 **ข้อสรุป**: ไม่มีแบบไหนดีกว่าแบบไหนเสมอไป วิศวกรที่ดีต้องรู้จักทั้งสองแบบ และเลือกใช้ให้เหมาะกับ requirement ของระบบนั้นๆ

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
