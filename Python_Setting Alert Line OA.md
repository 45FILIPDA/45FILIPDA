# การตั้งค่าระบบแจ้งเตือนผ่าน LINE Messaging API ด้วย Python (Complete Guide)

---

## ขั้นตอนที่ 1: การสร้างบัญชี LINE Official Account (LINE OA)

หากยังไม่มีบัญชี LINE OA สำหรับใช้งาน ให้ดำเนินการตามขั้นตอนดังนี้:
1. เข้าสู่ระบบที่ [LINE Official Account Manager](https://manager.line.biz/)
2. เลือก **สร้างบัญชี LINE Official Account**
3. กรอกข้อมูลรายละเอียดที่จำเป็น ได้แก่ ชื่อบัญชี, ประเภทธุรกิจ และอีเมล
4. ตรวจสอบความถูกต้องและกดยืนยันเพื่อสร้างบัญชี

---

## ขั้นตอนที่ 2: การเปิดใช้งาน Messaging API และการรับ Channel Access Token

Channel Access Token คือกุญแจสำคัญที่ใช้ยืนยันตัวตนว่าสคริปต์ Python มีสิทธิ์สั่งการบอทตัวนี้ สามารถหาได้ตามขั้นตอนดังนี้:
1. เข้าไปที่ [LINE Developers Console](https://developers.line.biz/console/)
2. สร้าง **Provider** ใหม่ (หรือเลือกอันที่มีอยู่) จากนั้นเลือกสร้าง Channel ประเภท **Messaging API** และเชื่อมโยงกับบัญชี LINE OA ที่สร้างไว้
3. คลิกเข้าไปที่ Channel ดังกล่าว แล้วเลือกแท็บ **Messaging API**
4. เลื่อนหน้าจอลงมาด้านล่างสุดที่หัวข้อ **Channel access token (long-lived)**
5. หากยังไม่มีให้กดปุ่ม **Issue** (ออกรหัส) จากนั้นคัดลอก (Copy) ข้อมูลชุดนี้เก็บไว้ (ข้อควรระวัง: ห้ามเปิดเผยข้อมูลส่วนนี้สู่สาธารณะ)

---

## ขั้นตอนที่ 3: การค้นหา LINE User ID

ระบบจำเป็นต้องใช้ User ID (รหัสที่ขึ้นต้นด้วยตัวอักษร U) ในการระบุตัวผู้รับข้อความ สามารถค้นหาได้ 4 วิธีหลัก:

**วิธีที่ 1: การหา User ID ของตนเอง (ในฐานะผู้พัฒนา / เจ้าของบอท)**
หากต้องการทดสอบระบบโดยการส่งข้อความเข้า LINE ส่วนตัวของผู้พัฒนาเอง:
1. เข้าไปที่ [LINE Developers Console](https://developers.line.biz/console/)
2. เลือก Provider และคลิกที่ Channel ของบอทที่ใช้งาน
3. ไปที่แท็บ **Basic settings**
4. เลื่อนลงมาด้านล่างสุดที่หัวข้อ **Your user ID**
5. คัดลอกรหัสที่แสดง (ขึ้นต้นด้วยตัว U) เพื่อนำไปใช้ทดสอบในระบบได้ทันที

**วิธีที่ 2: ผ่าน LINE OA Manager (สำหรับการดึงข้อมูลผู้ใช้อื่นเบื้องต้น)**
1. เข้าไปที่เมนู **Contact list** ทางแถบซ้ายมือในระบบ LINE OA Manager
2. เลือกรายชื่อผู้ใช้งานเป้าหมายที่เคยแอดบอทหรือทักข้อความมาแล้ว
3. ระบบจะแสดงข้อมูลโปรไฟล์ รวมถึง User ID ให้สามารถคัดลอกได้ทันที

**วิธีที่ 3: ผ่าน Webhook (สำหรับนักพัฒนา)**
1. สร้าง Webhook URL ชั่วคราวผ่านบริการรับข้อมูล (เช่น Webhook.site)
2. นำ URL ไปตั้งค่าใน LINE Developers Console ตรงช่อง Webhook URL
3. ให้ผู้ใช้งานเป้าหมายส่งข้อความหาบัญชี LINE OA
4. ตรวจสอบข้อมูล JSON ที่ส่งมายัง Webhook จะพบ User ID ระบุอยู่ในฟิลด์ `"userId"`

**วิธีที่ 4: การบันทึกลงฐานข้อมูล (สำหรับระบบองค์กร)**
1. สร้างระบบลงทะเบียนให้ผู้ใช้งานเชื่อมต่อบัญชี
2. เมื่อผู้ใช้งานดำเนินการสำเร็จ ระบบจะดึง User ID ผ่าน Webhook มาบันทึกลงในฐานข้อมูลกลางโดยอัตโนมัติ

---

## ขั้นตอนที่ 4: การจัดการสิทธิ์การเข้าถึงและความปลอดภัย

เพื่อความปลอดภัยของระบบและการจัดการข้อมูล ควรกำหนดสิทธิ์และป้องกันข้อมูลสำคัญดังนี้:

* **การจัดการบทบาทผู้ใช้งาน (Role-Based Access Control):**
  * **Administrator:** ให้สิทธิ์เฉพาะผู้รับผิดชอบหลักในการดูแล Token และตั้งค่าเชิงลึก
  * **Operator:** กำหนดสิทธิ์ให้ทีมงานทั่วไปสำหรับดูแลการตอบแชทหรือใช้งานฟังก์ชันพื้นฐาน โดยไม่สามารถเข้าถึงการตั้งค่า API ได้
* **การป้องกัน API Token:**
  * จัดเก็บ Channel Access Token และ User ID ไว้ในตัวแปรสภาพแวดล้อม (Environment Variables) เช่น ไฟล์ `.env`
  * ห้ามบันทึก Token หรือ User ID ลงใน Public Repository อย่างเด็ดขาด หากพบความเสี่ยงให้ดำเนินการ Revoke Token เดิมและกด Issue เพื่อสร้างใหม่ทันที

---

## ขั้นตอนที่ 5: สคริปต์ Python สำหรับส่งข้อความแจ้งเตือนตามเงื่อนไข

**คำแนะนำสำหรับการนำไปใช้งาน:**
* แทนที่ค่าในตัวแปร `LINE_TOKEN` ด้วย Channel Access Token ที่ได้รับจากขั้นตอนที่ 2
* แทนที่ค่าในตัวแปร `TARGET_USER_ID` ด้วย User ID ที่ได้รับจากขั้นตอนที่ 3
* โค้ดชุดนี้สามารถประยุกต์ใช้เพื่อแจ้งเตือนสถานะต่างๆ ภายในระบบตามเงื่อนไขที่กำหนด

```python
import requests

LINE_TOKEN = "YOUR_CHANNEL_ACCESS_TOKEN"
LINE_API_URL = "[https://api.line.me/v2/bot/message/push](https://api.line.me/v2/bot/message/push)"

def send_line_notification(user_id, message_text):
    headers = {
        "Content-Type": "application/json",
        "Authorization": f"Bearer {LINE_TOKEN}"
    }
    
    payload = {
        "to": user_id,
        "messages": [
            {
                "type": "text",
                "text": message_text
            }
        ]
    }
    
    response = requests.post(LINE_API_URL, headers=headers, json=payload)
    
    if response.status_code == 200:
        print("Success: Notification sent.")
    else:
        print(f"Error: {response.status_code}, {response.text}")

def conditional_alert(user_id, alert_type, data_value):
    if alert_type == "success":
        message = f"[SUCCESS] Operation completed: {data_value}"
    elif alert_type == "warning":
        message = f"[WARNING] Action required: {data_value}"
    elif alert_type == "error":
        message = f"[ERROR] System failure: {data_value}"
    else:
        message = f"[INFO] General notice: {data_value}"
        
    send_line_notification(user_id, message)

if __name__ == "__main__":
    TARGET_USER_ID = "YOUR_USER_ID"
    
    conditional_alert(TARGET_USER_ID, "success", "Database updated successfully.")
    conditional_alert(TARGET_USER_ID, "error", "Failed to connect to the server.")
