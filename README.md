# VTBD Tower · Flight Strips (ออนไลน์)

เกมเสิร์ฟเป็นไฟล์ static บน **GitHub Pages** และซิงก์ผู้เล่นผ่าน **Firebase Realtime Database**
(strips, METAR, นักบินที่บินอยู่, รายชื่อคนออนไลน์ — แยกตาม SEC A / SEC B)

## 1) สร้าง Firebase
1. https://console.firebase.google.com → **Add project** (ปิด Google Analytics ได้)
2. เมนู **Build → Realtime Database → Create database** → เลือก location (แนะนำ Singapore) → เริ่มด้วย *locked mode*
3. แท็บ **Rules** → วางเนื้อหาไฟล์ `database.rules.json` → **Publish**
4. **Project settings (ไอคอนเฟือง) → Your apps → Web (</>)** → Register app → คัดลอกค่า `firebaseConfig`
5. เปิด `firebase-config.js` แล้วแทนค่า `YOUR_...` ทั้งหมด (ต้องมี `databaseURL` ตามที่หน้า Realtime Database แสดง)

> `apiKey` ของ Firebase เว็บไม่ใช่ความลับ commit ขึ้น GitHub ได้ ความปลอดภัยอยู่ที่ Rules

## 2) ขึ้น GitHub Pages
1. สร้าง repo ใหม่ (public) แล้วอัปโหลดไฟล์ทั้งหมดในโฟลเดอร์นี้ (`index.html`, `firebase-config.js`, `.nojekyll`, ...)
2. **Settings → Pages → Build and deployment → Deploy from a branch → `main` / `(root)` → Save**
3. รอ 1–2 นาที เปิด `https://<username>.github.io/<repo>/`
4. ส่งลิงก์ให้เพื่อน เลือก SEC เดียวกัน แล้วเลือกตำแหน่ง (TWR / GND / ... / PILOT) ได้เลย

## สถานะการเชื่อมต่อ
มุมขวาล่างของเกมจะขึ้น `● LIVE · ออนไลน์ N` เมื่อเชื่อม Firebase สำเร็จ
ถ้าขึ้น `○ เล่นคนเดียว` แปลว่า `firebase-config.js` ยังไม่ถูกกรอก หรือโหลด Firebase ไม่ได้

## หมายเหตุด้านความปลอดภัย
Rules ชุดนี้ให้ทุกคนที่รู้ลิงก์อ่าน/เขียนข้อมูลเกมได้ (เหมาะกับห้องเล่นกับเพื่อน) และจำกัดเฉพาะ path ของเกมเท่านั้น
ถ้าต้องการเข้มขึ้น ให้เปิด Anonymous Authentication + App Check แล้วเปลี่ยน `.write` เป็น `auth != null`

## ทดสอบในเครื่อง
`python3 -m http.server 8000` แล้วเปิด http://localhost:8000
