# CCNA Homework LAB-X02

**รูปที่ 1:** กระบวนการ Boot ของ Router
![[Pasted image 20260424103654.png]]

> [!info] 🚀 กระบวนการ Boot ของ Router
> แสดงกระบวนการเปิดเครื่องของ Router ซึ่งกำลังทำการโหลดและแตกไฟล์ระบบปฏิบัติการ (IOS Image Load Test / Self decompressing the image) ลงในหน่วยความจำ (RAM)

**รูปที่ 2:** การเข้าโหมด ROMMON และข้ามการโหลด Startup Config
![[Pasted image 20260424103713.png]]

> [!warning] 🛠️ การเข้าโหมด ROMMON และข้ามการโหลด Startup Config
> เป็นขั้นตอนเริ่มของการทำ **Password Recovery** โดยการเข้าสู่โหมด ROMMON แล้วใช้คำสั่ง `confreg 0x2142` เพื่อเปลี่ยนค่า Configuration Register (สั่งให้ Router เปิดเครื่องโดยข้ามการอ่านไฟล์ตั้งค่าเดิมหรือ startup-config) จากนั้นสั่ง `boot` เพื่อรีสตาร์ท เมื่อเครื่องเปิดขึ้นมาจะถามว่าต้องการเข้าสู่ Configuration Dialog หรือไม่ ให้ตอบ `no`

**รูปที่ 3:** การดึงการตั้งค่าเดิมกลับมา
![[Pasted image 20260424103735.png]]

> [!note] 📥 การดึงการตั้งค่าเดิมกลับมา
> หลังจากเข้าเครื่องได้แล้ว (โดยไม่มีพาสเวิร์ด) เราจะใช้คำสั่ง `copy startup-config running-config` เพื่อคัดลอกไฟล์การตั้งค่าดั้งเดิมจาก NVRAM มาใส่ไว้ใน RAM ทำให้เราได้การตั้งค่าเดิม (เช่น ชื่อ hostname เป็น CCNA) กลับมาเพื่อเตรียมทำการแก้ไขพาสเวิร์ดต่อไป

**รูปที่ 4:** การตั้งรหัสผ่านใหม่
![[Pasted image 20260424103754.png]]

> [!success] 🔑 การตั้งรหัสผ่านใหม่
> ทำการสร้างบัญชีผู้ใช้และกำหนดรหัสผ่านใหม่เพื่อใช้เข้าเครื่อง โดยใช้คำสั่ง `username admin secret cisco` (สร้างผู้ใช้ admin รหัสผ่าน cisco) และเปลี่ยนรหัสผ่านสำหรับเข้า Privilege mode ใหม่ด้วยคำสั่ง `enable secret cisco`

**รูปที่ 5:** การคืนค่า Configuration Register และบันทึกการตั้งค่า
![[Pasted image 20260424103802.png]]

> [!success] 💾 การคืนค่า Configuration Register และบันทึกการตั้งค่า
> เปลี่ยนค่า Configuration Register กลับเป็นค่ามาตรฐานด้วยคำสั่ง `config-register 0x2102` (เพื่อให้เปิดเครื่องครั้งต่อไปดึงไฟล์การตั้งค่ามาใช้ตามปกติ) หลังจากนั้นออกจากโหมด config แล้วสั่งบันทึกการตั้งค่าทั้งหมดด้วย `copy running-config startup-config` (หรือคำสั่ง `write`) เพื่อให้รหัสผ่านใหม่ถูกบันทึกไว้ถาวร
[[Form @CCNA Homework LAB-X03]]
