# CCNA Homework LAB-X09: Dynamic Trunking Protocol (DTP)

**รูปที่ 1:** แผนผังเครือข่ายและการกำหนดโหมด DTP
![[Pasted image 20260424134353.png]]

> [!abstract] 📌 รายละเอียดโจทย์ (DTP Modes)
> ในแล็บนี้เราจะทดสอบการทำงานของ DTP ในโหมดต่างๆ เพื่อดูว่าพอร์ตจะกลายเป็น Trunk หรือไม่ โดยมีการกำหนดโหมดดังนี้:
> - **Dynamic Auto:** รอให้ฝั่งตรงข้ามมาร้องขอการเป็น Trunk
> - **Dynamic Desirable:** พยายามร้องขอฝั่งตรงข้ามให้เป็น Trunk
> - **Static Trunk (Nonegotiate):** บังคับเป็น Trunk และปิดการต่อรอง (ไม่ส่ง DTP Packet)

---

### 🛠 ขั้นตอนการกำหนดค่า DTP บน Switch
**รูปที่ 2:** คำสั่งการตั้งค่าในแต่ละ Task
![[Pasted image 20260424134336.png]]

> [!info] ⚙️ สรุปคำสั่งที่สำคัญ
> 1. **โหมด Dynamic Auto:** `switchport mode dynamic auto`
> 2. **โหมด Dynamic Desirable:** `switchport mode dynamic desirable`
> 3. **โหมด Static Trunk:** `switchport mode trunk`
> 4. **การปิดการต่อรอง (Nonegotiate):** `switchport nonegotiate` (ใช้ร่วมกับโหมด trunk เพื่อไม่ให้อีกฝั่งรู้ว่าเป็น DTP)

---

### 🔍 การตรวจสอบผลลัพธ์ (Verification)
**รูปที่ 3:** ตรวจสอบสถานะด้วยคำสั่ง show interfaces switchport
![[Pasted image 20260424134428.png]]

> [!success] ✅ ผลการทดสอบ
> จากการตรวจสอบด้วยคำสั่ง `show interfaces [Port] switchport` จะเห็นผลลัพธ์ที่น่าสนใจดังนี้:
> 
> - **พอร์ต Fa0/1 ของ SW1:** ตั้งค่าเป็น **dynamic auto** แต่สามารถทำงานเป็น **trunk** ได้สำเร็จ (Operational Mode: trunk) เพราะฝั่งตรงข้าม (SW3) เป็น desirable
> - **พอร์ต Fa0/1 ของ SW3:** ตั้งค่าเป็น **dynamic desirable** และทำงานเป็น **trunk** ได้สำเร็จ
> - **พอร์ต Fa0/3 ของ SW2:** ตั้งค่าเป็น **trunk** แบบปิดการต่อรอง (**Negotiation of Trunking: Off**) ทำให้พอร์ตนี้เป็น Trunk ตลอดเวลาโดยไม่มีการส่ง DTP Packet ไปรบกวน
> 
> **สรุปกฎการเกิด Trunk:** 
> - Desirable + Auto = **Trunk**
> - Desirable + Desirable = **Trunk**
> - Auto + Auto = **Access** (ไม่เกิด Trunk)
