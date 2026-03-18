# INDIVIDUAL_REPORT_67543210044-3.md

## ข้อมูลผู้จัดทำ
- ชื่อ-นามสกุล: ภานุวัฒน์ ต๋าคำ
- รหัสนักศึกษา: 67543210044-3
- กลุ่ม: 14

## ขอบเขตงานที่รับผิดชอบ
รับผิดชอบในส่วนของ **Auth Service**, **Nginx API Gateway**, การจัดการ **HTTPS Certificate** และการทำ **Database Initialization/Seed Users**

## สิ่งที่ได้ดำเนินการด้วยตนเอง
- **Nginx & HTTPS**: ตั้งค่า Nginx ให้ทำหน้าที่เป็น Reverse Proxy และ TLS Termination โดยใช้ Self-signed Certificate พร้อมทั้งทำระบบ Redirect จาก HTTP ไปยัง HTTPS 
- **Auth Service**: พัฒนา API สำหรับการ Login, Verify และการดึงข้อมูล Profile (Me) โดยใช้ JWT (jsonwebtoken)
- **Security**: ออกแบบระบบการตรวจสอบรหัสผ่านแบบ Timing-safe compare โดยใช้ `bcryptjs` และตั้งค่า Rate Limiting ใน Nginx เพื่อป้องกัน Brute-force
- **Database**: เขียนไฟล์ `init.sql` เพื่อกำหนด Schema ของตาราง `users` และเตรียม Seed Users (Alice, Bob, Admin) พร้อมรหัสผ่านที่ผ่านการ Hash
- **Logging Integration**: เขียนฟังก์ชัน `logEvent` ใน Auth Service เพื่อส่ง Log เหตุการณ์การ Login ไปยัง Log Service

## ปัญหาที่พบและวิธีการแก้ไข
- **ปัญหา**: Nginx ไม่ยอมทำงานเนื่องจากหาไฟล์ Certificate ไม่เจอในตอนแรก
- **การแก้ไข**: ตรวจสอบการทำ Volume Mount ใน `docker-compose.yml` และเขียนสคริปต์ `gen-certs.sh` เพื่อสร้างไฟล์ในโฟลเดอร์ที่ถูกต้องพร้อมกำหนด Permission ให้ Nginx อ่านได้

## สิ่งที่ได้เรียนรู้จากงานนี้
- ได้เรียนรู้การตั้งค่า **TLS Termination** บน Nginx ซึ่งเป็นหัวใจสำคัญของความปลอดภัยในระดับ Gateway
- เข้าใจกระบวนการทำงานของ **JWT flow** ตั้งแต่การสร้าง Token ไปจนถึงการ Verify ในแต่ละ Service
- เห็นข้อดีของการแยก **Auth Service** ออกจากกัน ทำให้การจัดการ Security ทำได้ง่ายและเป็นสัดส่วน

## แนวทางการพัฒนาต่อไปใน Set 2
- ควรแยกฐานข้อมูลของ Auth ออกเป็นอิสระ (Database-per-service) เพื่อลดการพึ่งพากัน (Loose Coupling)
- เพิ่มระบบ Register และ User Service แยกต่างหากเพื่อรองรับการขยายตัวของระบบในอนาคต
