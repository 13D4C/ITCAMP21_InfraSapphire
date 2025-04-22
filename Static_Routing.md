## ตั้งค่า Static Routing บน Cisco Router ❄️☃️🌨️

![image](https://github.com/user-attachments/assets/6923e066-105f-40ee-9f8c-96cd50c13261)

จากภาพ Topology ที่ให้มา เราจะตั้งค่า Static Route เพื่อให้ PC1 และ PC2 สามารถสื่อสารกันได้  โดยผ่าน Router1 และ Router2  ซึ่งเชื่อมต่อกันด้วยเส้นทางที่มี IP  10.30.6.1/30 และ 10.30.6.2/30

**ขั้นตอนการตั้งค่า Static Route บน Router1:**

1. **เข้าสู่ Configuration Mode:**
   ```
   Router1> enable
   Router1# configure terminal
   Router1(config)#
   ```

2. **กำหนด Static Route:** บอก Router1 ว่าถ้าจะไปยังเครือข่าย 192.168.2.0/24 (เครือข่ายของ PC2) ให้ส่งข้อมูลไปที่ Next Hop คือ 10.30.6.2 (IP ของ Router2)
   ```
   Router1(config)# ip route 192.168.2.0 255.255.255.0 10.30.6.2
   ```
   ❄️ เหมือนกับการปั้นตุ๊กตาหิมะบอกทาง ☃️ "ถ้าจะไปหา PC2 ต้องไปทางนี้! 👉 10.30.6.2"

3. **บันทึกการตั้งค่า:**
   ```
   Router1(config)# end
   Router1# copy running-config startup-config
   ```
   💾 เก็บเส้นทางไว้ เหมือนเก็บเกล็ดหิมะสวยๆ ไว้ในความทรงจำ!


**ขั้นตอนการตั้งค่า Static Route บน Router2:** (ทำเช่นเดียวกับ Router1 แต่ Next Hop จะเป็น 10.30.6.1 ซึ่งเป็น IP ของ Router1)

1. **เข้าสู่ Configuration Mode:**
   ```
   Router2> enable
   Router2# configure terminal
   Router2(config)#
   ```

2. **กำหนด Static Route:** บอก Router2 ว่าถ้าจะไปยังเครือข่าย 192.168.1.0/24 (เครือข่ายของ PC1) ให้ส่งข้อมูลไปที่ Next Hop คือ 10.30.6.1 (IP ของ Router1)
   ```
   Router2(config)# ip route 192.168.1.0 255.255.255.0 10.30.6.1
   ```
   🌨️ เหมือนกับเกล็ดหิมะบอกทาง ❄️ "ถ้าจะไปหา PC1 ต้องไปทางนี้!  👈 10.30.6.1"


3. **บันทึกการตั้งค่า:**
   ```
   Router2(config)# end
   Router2# copy running-config startup-config
   ```


**ตรวจสอบการตั้งค่า:**

* บน Router1: `show ip route` จะเห็น Static Route ที่เราตั้งค่าไว้
* บน Router2: `show ip route` จะเห็น Static Route ที่เราตั้งค่าไว้
* ทดสอบ Ping จาก PC1 ไปยัง PC2 และจาก PC2 ไปยัง PC1 เพื่อยืนยันว่าการเชื่อมต่อทำงานได้


**🎉 เสร็จสิ้น! การเดินทางของข้อมูลสำเร็จ!** 🎉 เหมือนกับการเล่นสกีลงเขาอย่างสนุกสนาน  ข้อมูลสามารถเดินทางจาก PC1 ไปยัง PC2 และกลับกันได้อย่างราบรื่นแล้ว! 🏂⛷️❄️☃️🌨️
