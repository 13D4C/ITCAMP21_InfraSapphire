## คำนวณ Subnet แบบละเอียด เหมือนหิมะโปรยปราย ❄️🌨️☃️

มาเรียนรู้การคำนวณ Subnet อย่างละเอียด พร้อมอิโมจิธีมหิมะกันเลย!  เหมือนเกล็ดหิมะที่ไม่เหมือนกัน แต่ละ Subnet ก็มีเอกลักษณ์เฉพาะตัว  ไปดูกันเลย! 

**สิ่งที่ต้องรู้ก่อนเริ่ม:**

* **IP Address:** ประกอบด้วย 32 บิต แบ่งเป็น 4 Octet คั่นด้วยจุด (.)  เช่น 192.168.1.10
* **Subnet Mask:** ใช้แบ่ง IP Address ออกเป็นส่วน Network และส่วน Host  เขียนในรูปแบบ Dotted Decimal  เช่น 255.255.255.0  หรือ CIDR Notation เช่น /24
* **Binary:** ระบบเลขฐานสอง มีแค่ 0 และ 1  สำคัญมากในการคำนวณ Subnet


**ขั้นตอนการคำนวณ Subnet:**

1. **แปลง IP Address และ Subnet Mask เป็น Binary:**
   * **ตัวอย่าง:** IP Address: 192.168.1.10 , Subnet Mask: 255.255.255.224 (/27)
   ```
   IP Address:   11000000.10101000.00000001.00001010
   Subnet Mask:  11111111.11111111.11111111.11111000  (/27 หมายถึงมี 1 จำนวน 27 บิต)
   ```  
   ☃️ เหมือนเรียงเกล็ดหิมะเป็นแถวเลย!

2. **หา Network Address:** ทำ AND Operation ระหว่าง IP Address และ Subnet Mask  (AND: ถ้าทั้งคู่เป็น 1 ผลลัพธ์เป็น 1, นอกนั้นเป็น 0)
   ```
   11000000.10101000.00000001.00001010  (IP Address)
   11111111.11111111.11111111.11111000  (Subnet Mask)
   ----------------------------------
   11000000.10101000.00000001.00001000  (Network Address) 
   ```
   ❄️ ได้ Network Address เป็น 192.168.1.8 แล้ว!

3. **หา Broadcast Address:**
   * เปลี่ยนบิตในส่วน Host ของ Network Address ทั้งหมดเป็น 1
   ```
   11000000.10101000.00000001.00001000 (Network Address)
   ส่วน Host คือ 3 บิตสุดท้าย  เปลี่ยนเป็น 1 --> 111
   ผลลัพธ์: 11000000.10101000.00000001.00001111 (Broadcast Address)
   ```
   🌨️ ได้ Broadcast Address เป็น 192.168.1.31 แล้ว!

4. **หา Usable Host Range:**  IP ที่ใช้งานได้จริงใน Subnet นั้นๆ
   * เริ่มจาก Network Address + 1  
   * จบที่ Broadcast Address - 1
   * **ตัวอย่าง:** 192.168.1.9 - 192.168.1.30


5. **จำนวน Host ที่ใช้งานได้:** คำนวณจาก 2<sup>n</sup> - 2  (n คือจำนวนบิตในส่วน Host)
   * **ตัวอย่าง:**  ส่วน Host มี 3 บิต  2<sup>3</sup> - 2 = 6


**สรุปผล:**

* **Network Address:** 192.168.1.8
* **Broadcast Address:** 192.168.1.31
* **Usable Host Range:** 192.168.1.9 - 192.168.1.30
* **จำนวน Host ที่ใช้งานได้:** 6

หวังว่าจะเข้าใจการคำนวณ Subnet มากขึ้นนะครับ!  เหมือนหิมะที่ค่อยๆ โปรยปรายลงมา  ❄️🌨️☃️  สู้ๆ นะครับ!

Tool สำหรับการคำนวน Subnet ง่ายๆ : https://www.calculator.net/ip-subnet-calculator.html

## ตั้งค่า IP Address ใน Cisco Router ท่ามกลางหิมะโปรยปราย ❄️🌨️☃️

มาเรียนรู้วิธีตั้งค่า IP Address ใน Cisco Router อย่างละเอียด พร้อม Topology ประกอบ และอิโมจิธีมหิมะสุดน่ารักกันเถอะ! เหมือนกับการสร้างเส้นทางเชื่อมต่อท่ามกลางหิมะขาวโพลน แต่ละขั้นตอนสำคัญเหมือนเกล็ดหิมะที่เชื่อมต่อกันเป็นผลึกสวยงาม

**Topology:**

![image](https://github.com/user-attachments/assets/4d441fa2-5693-4754-915b-0c825c0bafb7)


ใน Topology นี้ เราจะตั้งค่า IP Address ให้กับ Interface ของ Router (R1) ที่เชื่อมต่อกับ PC1 และ PC2  

**ขั้นตอนการตั้งค่า IP Address:**

1. **เข้าสู่ Router:**  ใช้โปรแกรมจำลองเช่น Packet Tracer หรือ GNS3 เชื่อมต่อกับ Router ผ่าน Console Port  หรือใช้ SSH/Telnet ถ้าเปิดใช้งานอยู่  
   *(เหมือนเราเดินลุยหิมะไปหา Router)* 🚶❄️

2. **เข้าสู่ Privilege Exec Mode:** พิมพ์ `enable` แล้วกด Enter  
    *(เหมือนไขกุญแจเข้าบ้าน)* 🗝️

3. **เข้าสู่ Global Configuration Mode:** พิมพ์ `configure terminal` หรือ `conf t` แล้วกด Enter
    *(เหมือนเข้าไปตกแต่งบ้าน)* 🏡

4. **เข้าสู่ Interface Configuration Mode:** พิมพ์ `interface <interface>` แล้วกด Enter  โดย `<interface>` คือชื่อ Interface ที่ต้องการตั้งค่า เช่น `interface GigabitEthernet0/0` (สำหรับเชื่อมต่อ PC1)  
    *(เหมือนเลือกห้องที่จะตกแต่ง)* 🚪

5. **กำหนด IP Address และ Subnet Mask:** พิมพ์ `ip address <ip_address> <subnet_mask>` แล้วกด Enter เช่น `ip address 192.168.1.1 255.255.255.0`
    *(เหมือนทาสีห้อง)* 🎨

6. **เปิดใช้งาน Interface:** พิมพ์ `no shutdown` แล้วกด Enter
    *(เหมือนเปิดไฟในห้อง)*💡

7. **ออกจาก Interface Configuration Mode:** พิมพ์ `exit` แล้วกด Enter
    *(เหมือนออกจากห้องที่ตกแต่งเสร็จแล้ว)* 🚪

8. **ทำซ้ำขั้นตอนที่ 4-7 สำหรับ Interface อื่นๆ:**  เช่น Interface ที่เชื่อมต่อกับ PC2  อาจใช้ IP Address 192.168.2.1 255.255.255.0
    *(เหมือนไปตกแต่งห้องอื่นๆ)* 🏠🎨💡

9. **บันทึกการตั้งค่า:** พิมพ์ `copy running-config startup-config` หรือ `wr` แล้วกด Enter เพื่อบันทึกการตั้งค่าลง NVRAM  
    *(เหมือนเซฟรูปบ้านที่ตกแต่งเสร็จแล้ว)* 💾

10. **ตรวจสอบการตั้งค่า:** พิมพ์ `show ip interface brief` เพื่อดู IP Address ที่ตั้งค่าไว้ในแต่ละ Interface  
   *(เหมือนเดินสำรวจบ้านที่ตกแต่งเสร็จ)* 🚶‍♂️🏡


**ตัวอย่างคำสั่ง:**

```cisco
enable
configure terminal
interface GigabitEthernet0/0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit
interface GigabitEthernet0/0/1
ip address 192.168.2.1 255.255.255.0
no shutdown
exit
copy running-config startup-config
show ip interface brief 
```

**(เสร็จแล้ว! เหมือนเราได้สร้างเส้นทางเชื่อมต่อท่ามกลางหิมะที่สวยงาม)* 🎉❄️☃️🌨️


**หมายเหตุ:**  

* ภาพ Topology เป็นเพียงตัวอย่าง  อาจมีการเชื่อมต่อและอุปกรณ์ที่แตกต่างกันไปในแต่ละสถานการณ์
* คำสั่งและ Interface อาจแตกต่างกันไป ขึ้นอยู่กับรุ่นของ Router  ควรศึกษาคู่มือของ Router รุ่นที่ใช้งานประกอบด้วย


หวังว่าคำอธิบายนี้จะช่วยให้เข้าใจการตั้งค่า IP Address ใน Cisco Router ได้อย่างชัดเจนนะครับ! 😊  เหมือนหิมะที่โปรยปรายลงมาอย่างสวยงามและนุ่มนวล  ❄️🌨️☃️

