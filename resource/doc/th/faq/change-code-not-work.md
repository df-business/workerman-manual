# การไม่ได้แก้ไขโค้ดหลังจากการเปลี่ยนแปลง

**เหตุผล:**

Workerman เป็นการทำงานอยู่ในหน่วยความจำตลอดเวลา ซึ่งทำให้สามารถหลีกเลี่ยงการอ่านข้อมูลจากดิสก์ซ้ำๆ และการแปลงรหัส PHP ซ้ำๆ ซึ่งทำให้มีประสิทธิภาพที่สุด ดังนั้น เมื่อมีการเปลี่ยนแปลงโค้ดธุรกิจจำเป็นต้องโหลดโหมดรีโหลดหรือรีสตาร์ทเพื่อให้สามารถใช้งานได้

ในทำเสร็จ workerman ยังมีการให้บริการตรวจสอบไฟล์ที่อัปเดต เมื่อมีการตรวจจับว่ามีการอัปเดตไฟล์ จะโหลดโหมดรีโหลดโดยอัตโนมัติ โดยการนำไปใช้งานพร้อมโปรเจคเมื่อเริ่มต้น

โนโต: ระบบปฏิบัติการของ Windows ไม่รองรับการโหมดรีโหลด ดังนั้นไม่สามารถใช้บริการตรวจสอบไฟล์ได้

**ลิงก์ดาวน์โหลดบริการตรวจสอบไฟล์:**

1. เวอร์ชันที่ไม่มีการขึ้นอยู่: https://github.com/walkor/workerman-filemonitor

2. เวอร์ชันที่มีการขึ้นอยู่: https://github.com/walkor/workerman-filemonitor-inotify

**ความแตกต่างระหว่างสองเวอร์ชัน:**

เวอร์ชัน 1 ใช้วิธีการตรวจสอบเวลาอัปเดตไฟล์ทุกวินาทีเพื่อดูว่าไฟล์มีการอัปเดตหรือไม่

เวอร์ชัน 2 ใช้อินินูตเพื่อกลไกการแจ้งเตือนในเคอร์เนลของ Linux โดยระบบจะแจ้งเตือนเมื่อมีการอัปเดตไฟล์

โดยทั่วไปการใช้เวอร์ชัน 1 ที่ไม่มีการขึ้นอยู่นั้นเพียงพอแล้ว