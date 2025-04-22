## ตั้งค่า Static NAT บน Cisco Router ❄️☃️🌨️

![image](https://github.com/user-attachments/assets/409929de-7cd4-4d25-950b-cc15e5d124ac)

**ขั้นตอนการตั้งค่า Static NAT :**

1. **กำหนด Interface ที่เป็น Inside และ Outside:**
   ```
   Router1(config)# interface GigabitEthernet0/0  // Interface ที่เชื่อมต่อกับ PC1 (Inside)
   Router1(config-if)# ip nat inside
   Router1(config-if)# exit

   Router1(config)# interface GigabitEthernet0/1 // Interface ที่เชื่อมต่อกับ Cloud (Outside)
   Router1(config-if)# ip nat outside
   Router1(config-if)# exit
   ```
    🌐 กำหนดประตูบ้านหิมะเหมือนเดิม!  Inside เชื่อมต่อกับ PC1 🏘️ และ Outside เชื่อมต่อกับ Cloud ☁️


2. **กำหนด Static NAT:**  แปลง IP ภายใน (192.168.1.2 ของ PC1) เป็น IP ภายนอก (10.30.6.207)
   ```
   Router1(config)# ip nat inside source static 192.168.1.2 10.30.6.207
   ```
   ☃️ สร้างอุโมงค์หิมะเฉพาะ! ❄️ เชื่อมต่อ IP ภายนอกกับ IP ของ PC1 โดยตรง  ไม่มีการแชร์กับใคร


3. **บันทึกการตั้งค่า:**
   ```
   Router1(config)# end
   Router1# copy running-config startup-config
   ```
   💾 เซฟการตั้งค่า เหมือนเก็บหิมะไว้ในตู้เย็นให้คงความเย็นไว้!


**ตรวจสอบการตั้งค่า:**

* `show ip nat translations`  ดูว่ามีการแปลง IP ของ PC1 เป็น 10.30.6.207 หรือไม่
* `show ip nat statistics` ดูสถิติการทำงานของ NAT


**🎉 เสร็จสิ้น! PC1 มีทางออกส่วนตัวไปเล่นหิมะแล้ว!** 🎉 ตอนนี้ PC1 สามารถเชื่อมต่ออินเทอร์เน็ตได้โดยใช้ Public IP Address ที่กำหนดไว้โดยเฉพาะ  ไม่มีการแชร์กับอุปกรณ์อื่น  เหมือนมีทางลาดหิมะส่วนตัว! 🏂❄️☃️🌨️  


**ข้อควรระวัง:** การไม่ใช้ Overload เหมาะกับกรณีที่มี Public IP Address เพียงพอต่อจำนวนอุปกรณ์ที่ต้องการ NAT  ถ้า Public IP Address ไม่เพียงพอ ควรพิจารณาใช้วิธีอื่นเช่น PAT หรือ Dynamic NAT


