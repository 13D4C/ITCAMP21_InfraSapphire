## ตั้งค่า SSH/Telnet บน Cisco Router และ Switch ❄️☃️🌨️

มาเรียนรู้การตั้งค่า SSH/Telnet บน Cisco Router และ Switch พร้อมอิโมจิธีมหิมะสุดน่ารักกันเลย! เหมือนกับการสร้างประตูวิเศษ 🚪✨ ที่จะให้เราเข้าไปควบคุมอุปกรณ์จากระยะไกลได้

**ข้อควรระวัง:** Telnet ส่งข้อมูลแบบ Plain Text (ไม่เข้ารหัส)  จึงมีความเสี่ยงด้านความปลอดภัยสูง  **แนะนำให้ใช้ SSH ซึ่งเข้ารหัสข้อมูลและปลอดภัยกว่า**


**ขั้นตอนการตั้งค่า SSH บน Cisco Router/Switch:**

1. **ตั้งค่า Hostname และ Domain Name:** (จำเป็นสำหรับ SSH)
   ```
   Router(config)# hostname Router1  
   Router(config)# ip domain-name yourdomain.com
   ```
   ✨ ตั้งชื่อให้ Router เหมือนตั้งชื่อ Snowman! ☃️

2. **สร้าง RSA Key:** ใช้สำหรับการเข้ารหัส  (ยิ่ง Key Size มาก ยิ่งปลอดภัย)
   ```
   Router(config)# crypto key generate rsa general-keys modulus 2048 
   ```
    🔑 สร้างกุญแจวิเศษสำหรับเปิดประตู SSH!

3. **กำหนด Line Configuration สำหรับการเชื่อมต่อระยะไกล (VTY Lines):**
   ```
   Router(config)# line vty 0 15  //กำหนด Line สำหรับการเชื่อมต่อ SSH/Telnet จำนวน 16 lines
   Router(config-line)# transport input ssh  //อนุญาตเฉพาะ SSH
   Router(config-line)# login local //กำหนดการ loginแบบ local ใช้ username/password ที่สร้างไว้ใน router
    Router(config-line)# exit
   ```
   🚪 กำหนดประตูสำหรับเข้าใช้งาน SSH!

4. **เปิดใช้งาน AAA (ถ้าต้องการ):** เพื่อจัดการ Username/Password  (ขั้นตอนนี้ไม่บังคับ ถ้าใช้ `login local`  สามารถข้ามไปขั้นตอนที่ 5 ได้เลย)
   ```
   Router(config)# aaa new-model
   Router(config)# aaa authentication login default local 
   ```
    👮‍♂️ กำหนดคนเฝ้าประตู (Authentication) สำหรับ SSH!

5. **บันทึกการตั้งค่า:**
   ```
   Router(config)# end
   Router# copy running-config startup-config
   ```
    💾 บันทึกการตั้งค่า เหมือนบันทึกเรื่องราวการผจญภัยในดินแดนมหัศจรรย์หิมะ!


**ขั้นตอนการตั้งค่า Telnet บน Cisco Router/Switch (ไม่แนะนำ):**

1. **กำหนด Line Configuration:**
   ```
   Router(config)# line vty 0 15
   Router(config-line)# transport input telnet // อนุญาต Telnet (ไม่ปลอดภัย)
   Router(config-line)# login local  // ใช้ local username/password
   Router(config-line)# exit
   ```
   🔓 เปิดประตู Telnet (ไม่ปลอดภัย ระวัง Monster 👾!)

2. **บันทึกการตั้งค่า:**
    ```
    Router(config)# end
    Router# copy running-config startup-config
    ```


**ตรวจสอบการตั้งค่า:**

* `show ip ssh` :  ดูรายละเอียดการตั้งค่า SSH
* `show running | include line vty` : ดูการตั้งค่า Line VTY
* `show running | include aaa` : ดูการตั้งค่า AAA (ถ้ามี)



**🎉 เสร็จสิ้น! ประตู SSH/Telnet พร้อมใช้งานแล้ว!** 🎉  ตอนนี้คุณสามารถเข้าถึง Router/Switch ผ่าน SSH/Telnet จากระยะไกลได้แล้ว!  เหมือนกับการใช้เวทมนตร์เดินทางข้ามหิมะไปยัง Router/Switch ได้อย่างง่ายดาย! ✨🧙‍♂️❄️☃️🌨️


**หมายเหตุ:**

*  อย่าลืมกำหนด Username/Password บน Router/Switch ก่อน  โดยใช้คำสั่ง `username <username> password <password> privilege 15` ใน Global Configuration Mode.
*  ตรวจสอบ Firewall ว่าอนุญาตการเชื่อมต่อ SSH/Telnet หรือไม่.  Port SSH คือ 22, Port Telnet คือ 23.



