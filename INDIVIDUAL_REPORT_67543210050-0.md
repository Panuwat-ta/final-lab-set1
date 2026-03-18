# INDIVIDUAL_REPORT_67543210050-0.md

## ข้อมูลผู้จัดทำ
- ชื่อ-นามสกุล: เอกพันธ์ ทศทิศรังสรรค์
- รหัสนักศึกษา: 67543210050-0
- กลุ่ม: 14

## ขอบเขตงานที่รับผิดชอบ
รับผิดชอบในส่วนของ **Task Service**, **Log Service**, การพัฒนา **Frontend (index.html, logs.html)** และการควบคุม **Docker Compose integration**

## สิ่งที่ได้ดำเนินการด้วยตนเอง
- **Task Service**: พัฒนา CRUD API ทั้งหมด โดยมีการทำระบบ **Owner-only access** (พนักงานแก้ไขได้เฉพาะงานของตนเอง) และเพิ่มสิทธิ์ให้ Admin เห็นงานทั้งหมดได้
- **Log Service**: สร้าง Service ส่วนกลางสำหรับเก็บ Log โดยใช้ PostgreSQL และพัฒนา Endpoint เพื่อคำนวณสถิติ (Stats) ส่งไปยัง Dashboard
- **Frontend Development**: 
    - ปรับปรุงหน้า `index.html` (Task Board) ให้รองรับการเชื่อมต่อแบบ Microservices และแสดงชื่อผู้ใช้งานที่ดึงมาจากตาราง Users
    - พัฒนาหน้า `logs.html` (Log Dashboard) ใหม่ทั้งหมด เพื่อใช้ในการมอนิเตอร์สถานะระบบและดู Log ย้อนหลัง
- **Middleware**: เขียน **authMiddleware** เพื่อตรวจสอบความถูกต้องของ JWT ในทุกๆ Request ที่ส่งมายัง Task Service
- **Docker Orchestration**: ปรุงแต่งไฟล์ `docker-compose.yml` ให้คอนเทนเนอร์ทั้งหมด 6 ตัว สื่อสารกันได้ผ่าน Docker Network

## ปัญหาที่พบและวิธีการแก้ไข
- **ปัญหา**: การแสดงรายการ Task ไม่แสดงชื่อผู้เขียน และ API เดิมใช้ฟิลด์ `name` แต่ในตาราง User ใช้ `username`
- **การแก้ไข**: ทำการสั่ง JOIN ตาราง `tasks` กับ `users` ใน SQL Query และปรับปรุง Frontend ให้ใช้ฟิลด์ `username` ให้ตรงกันทั้งระบบ

## สิ่งที่ได้เรียนรู้จากงานนี้
- เข้าใจสถาปัตยกรรม **Microservices** ในเชิงปฏิบัติ โดยเฉพาะการสื่อสารระหว่างกันหลัง Nginx Proxy
- เรียนรู้การทำ **Centralized Logging** ซึ่งมีประโยชน์มากในการ Debug ระบบที่มีหลาย Service ทำงานพร้อมกัน
- ฝึกทักษะการแยกสิทธิ์ (RBAC) ระหว่าง Member และ Admin ในระบบจริง

## แนวทางการพัฒนาต่อไปใน Set 2
- ควรเปลี่ยนจากการใช้ Shared Database ไปเป็นแบบ **Database-per-service** เพื่อให้แต่ละ Service มีอิสระต่อกันอย่างแท้จริง
- เพิ่มระบบการทำ CI/CD และการส่ง Log ไปยัง External Platform อย่าง Grafana โดยใช้ Loki เพื่อการมอนิเตอร์ที่เป็นสากลยิ่งขึ้น
