# TEAM_SPLIT.md

## Team Members
- 67543210044-3 นาย ภานุวัฒน์ ต๋าคำ
- 67543210050-0 นาย เอกพันธ์ ทศทิศรังสรรค์

## Work Allocation

### Student 1: นาย ภานุวัฒน์ ต๋าคำ (67543210044-3)
- Auth Service (login route, JWT utils, logEvent)
- HTTPS Certificate + Nginx config
- db/init.sql + Seed Users

### Student 2: นาย เอกพันธ์ ทศทิศรังสรรค์ (67543210050-0)
- Task Service (CRUD routes, authMiddleware)
- Log Service
- Frontend (index.html + logs.html)
- Docker Compose integration

## Shared Responsibilities
- Architecture diagram
- End-to-end testing
- README + screenshots

## Integration Notes
- ระบบมีการเชื่อมต่อกันผ่าน Shared PostgreSQL Database โดยใช้ตาราง `users`, `tasks`, และ `logs` ร่วมกัน
- มีการใช้ Nginx เป็น API Gateway ในการทำ Reverse Proxy และจัดการ HTTPS
- ทุก Service รองรับระบบ JWT Authentication แบบเดียวกันเพื่อให้สามารถยืนยันตัวตนข้าม Service ได้
- Backend ทุกตัวมีการเรียกใช้ Log Service ภายใน Docker Network เพื่อบันทึกเหตุการณ์สำคัญแบบ Real-time