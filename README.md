# โครงการ IoT: โครงงานถุงมืออัจฉริยะเชื่อมโยงการสื่อสารระหว่าง ผู้บกพร่องทางการได้ยินและคนทั่วไป

โครงการนี้เป็นการผสมผสานระหว่าง Frontend (React), Backend (Node.js) และไมโครคอนโทรลเลอร์ ESP32 เพื่อการตรวจจับข้อมูลจากเซ็นเซอร์ Flex และ Gyro และส่งข้อมูลไปยัง API บนคลาวด์


## โครงสร้างของโปรเจกต์
- **Frontend**: โค้ดสำหรับ Frontend (อยู่ในไฟล์ `app.js`)
- **Backend**: [backend-iot](https://github.com/HelloArtty/backend-iot)
- **ESP32 Firmware**: โค้ดสำหรับ ESP32 (อยู่ในไฟล์ `message.cpp`)

---

## การเริ่มต้นใช้งาน

### Frontend (React)
#### ข้อกำหนดเบื้องต้น
- Node.js (เวอร์ชัน 14 ขึ้นไป)
- npm หรือ yarn

#### การตั้งค่า
1. สร้างโปรเจกต์ใหม่ด้วย Create React App:
   ```bash
   npx create-react-app frontend
   cd frontend
   ```
2. ติดตั้ง Dependencies:
   ```bash
   npm install
   ```
3. เริ่มเซิร์ฟเวอร์สำหรับพัฒนา:
   ```bash
   npm start
   ```
4. เปิดเบราว์เซอร์และไปที่ `http://localhost:3000`

---

### Backend (Node.js)
#### ข้อกำหนดเบื้องต้น
- Node.js (เวอร์ชัน 14 ขึ้นไป)
- npm

#### การตั้งค่า
1. โคลน Repository:
   ```bash
   git clone https://github.com/HelloArtty/backend-iot.git
   cd backend-iot
   ```
2. ติดตั้ง Dependencies:
   ```bash
   pip install requirements.txt
   ```
3. เริ่มเซิร์ฟเวอร์:
   ```bash
   python app.py
   ```
4. Backend จะทำงานที่ `http://localhost:5000` ตามค่าเริ่มต้น

---

### ESP32 Firmware
#### ข้อกำหนดเบื้องต้น
- Arduino IDE
- ไลบรารีบอร์ด ESP32

#### การตั้งค่า
1. ติดตั้งไลบรารีที่จำเป็นใน Arduino IDE:
   - `Wire`
   - `I2Cdev`
   - `MPU6050`
   - `WiFi`
   - `HTTPClient`

2. ตั้งค่าข้อมูล Wi-Fi ในเฟิร์มแวร์:
   ```cpp
   const char* ssid = "your-SSID";
   const char* password = "your-PASSWORD";
   ```

3. อัปโหลดเฟิร์มแวร์ (`message.cpp`) ไปยัง ESP32
   - ตรวจสอบให้แน่ใจว่าได้เลือกบอร์ดและพอร์ต COM ที่ถูกต้องใน Arduino IDE

4. ESP32 จะเชื่อมต่อกับ Wi-Fi และเริ่มส่งข้อมูลจากเซ็นเซอร์ไปยัง API Endpoint:
   ```cpp
   const char* serverURL = "https://backend-iot-gdaq.onrender.com/predict";
   ```

---

## การทำงานของระบบ
1. **ESP32** อ่านข้อมูลจากเซ็นเซอร์ (Flex และ Gyro) และคำนวณค่าเฉลี่ยหลังจากอ่านข้อมูล 100 ครั้ง
2. ข้อมูลที่ประมวลผลจะถูกส่งไปยัง **Backend API** ในรูปแบบ JSON
3. **Backend** จัดเก็บและประมวลผลข้อมูล โดยให้บริการ Endpoint สำหรับการแสดงผล
4. **Frontend** ดึงข้อมูลจาก API และแสดงผลแบบเรียลไทม์

---
