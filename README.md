# Lerning Linux Audit Daemon

auditd (Linux Audit Daemon) เป็นโปรแกรมในระบบ Linux ที่ทำหน้าที่ติดตามและบันทึกเหตุการณ์ต่างๆ ในระดับเคอร์เนล เช่น การเข้าถึงไฟล์, การเรียกใช้งานคำสั่ง, และการเปลี่ยนแปลงระบบความปลอดภัย เพื่อใช้ในการตรวจสอบ (Audit) และวิเคราะห์ความปลอดภัย [1, 2, 3, 4] 
## ⚙️ องค์ประกอบหลัก

* auditd: ดีมอนที่ทำหน้าที่เขียนบันทึก (Logs) ลงดิสก์
* auditctl: เครื่องมือสำหรับเพิ่ม/ลบ หรือแก้ไขกฎการตรวจสอบ (Rules)
* ausearch: เครื่องมือสำหรับค้นหาและกรองข้อมูลในล็อก
* aureport: เครื่องมือสำหรับสรุปรายงานและดูภาพรวมของเหตุการณ์ [1, 3, 5] 

## 📂 ไฟล์การตั้งค่าที่สำคัญ

* กฎการทำงานหลัก: /etc/audit/auditd.conf
* ตำแหน่งเก็บกฎที่กำหนดเอง: /etc/audit/rules.d/audit.rules
* ไฟล์บันทึก (Logs): /var/log/audit/audit.log [3, 5, 6] 

## 🛠️ ตัวอย่างการใช้งาน
1. การตั้งค่าเฝ้าระวังไฟล์ (File Watch Rule)
สามารถเพิ่มกฎเพื่อตรวจสอบการเปลี่ยนแปลงไฟล์หรือไดเรกทอรีได้โดยใส่บรรทัดนี้ใน /etc/audit/rules.d/audit.rules
-w /etc/passwd -p wa -k passwd_change [3] 

* -w: กำหนดไฟล์/โฟลเดอร์ที่ต้องการมอนิเตอร์
* -p wa: ดักจับเฉพาะการเขียน (Write) และการเปลี่ยนสิทธิ์ (Attribute change)
* -k: กำหนดคีย์เวิร์ด (Key) เพื่อให้ค้นหาได้ง่ายขึ้น [3] 

2. การค้นหาเหตุการณ์
ใช้ ausearch เพื่อค้นหาตามคีย์เวิร์ดที่ระบุไว้
sudo ausearch -k passwd_change [3] 
อ่านข้อมูลเชิงลึกเพิ่มเติมเกี่ยวกับการกำหนดค่า กฎมาตรฐาน และการปรับแต่งระดับสูงได้จาก [Red Hat System Auditing](https://www.redhat.com/en/blog/configure-linux-auditing-auditd) หรือดูตัวอย่าง [GitHub Best Practice Auditd Configuration](https://github.com/neo23x0/auditd) [7] 

[1] [https://sematext.com](https://sematext.com/glossary/auditd/)
[2] [https://www.elastic.co](https://www.elastic.co/security-labs/linux-detection-engineering-with-auditd)
[3] [https://insiderthreatmatrix.org](https://insiderthreatmatrix.org/detections/DT037)
[4] [https://medium.com](https://medium.com/@mansour.mohamedaziz/linux-system-auditing-with-auditd-custom-rules-and-configuration-part-1-330e5a77123a)
[5] [https://linux.die.net](https://linux.die.net/man/8/auditd)
[6] [https://www.reddit.com](https://www.reddit.com/r/linux4noobs/comments/1f9oylf/help_understanding_auditd/?tl=th)
[7] [https://github.com](https://github.com/neo23x0/auditd)


INSTALL => https://github.com/wachira90/install-auditd
