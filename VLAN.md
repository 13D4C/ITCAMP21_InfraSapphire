## ตั้งค่า VLAN บน Switch ฉบับละเอียด พร้อม Topology หิมะโปรยปราย ❄️☃️🌨️

มาเรียนรู้วิธีตั้งค่า VLAN บน Switch อย่างละเอียด พร้อมภาพ Topology และอิโมจิธีมหิมะตกแต่งให้อ่านสนุกกันเถอะ! เหมือนเกล็ดหิมะที่เชื่อมต่อกันเป็นผืนใหญ่ VLAN ก็เชื่อมโยงอุปกรณ์ในเครือข่ายเข้าด้วยกันในลักษณะเดียวกัน

**Topology:**

![image](https://github.com/user-attachments/assets/136a8233-690c-48f1-9227-c35f42000af7)



**สถานการณ์:** เราจะแบ่งเครือข่ายออกเป็น 2 VLAN:

* **VLAN 10:** สำหรับ PC1(ฝ่ายขาย) ➡️💰
* **VLAN 20:** สำหรับ PC2(ฝ่ายบัญชี) ➡️📊


**ขั้นตอนการตั้งค่า VLAN บน Switch (SW1 และ SW2):**

1. **เข้าสู่โหมด Configuration:**
   ```cisco
   enable                  // เข้าสู่ Privileged EXEC mode
   configure terminal       // เข้าสู่ Global Configuration mode
   ```

2. **สร้าง VLAN:**
   ```cisco
   vlan 10                 // สร้าง VLAN 10
   name Sales              // ตั้งชื่อ VLAN (ไม่บังคับ แต่ช่วยให้จำง่าย)
   !
   vlan 20                 // สร้าง VLAN 20
   name Accounting         // ตั้งชื่อ VLAN
   exit                    // ออกจาก VLAN Configuration mode
    ```
    ☃️ เหมือนสร้างก้อนหิมะแยกกันสองก้อน!

3. **กำหนด Port ให้กับ VLAN:**  (ทำทั้งบน SW1 และ SW2)
   ```cisco
   interface FastEthernet0/2 //  Port ที่เชื่อมต่อกับ PC1
   switchport mode access     // กำหนดโหมด Port เป็น Access mode
   switchport access vlan 10  // กำหนด Port ให้อยู่ใน VLAN 10
   no shutdown                // เปิดใช้งาน Port
   !
   interface FastEthernet0/3 // Port ที่เชื่อมต่อกับ PC2
   switchport mode access
   switchport access vlan 10
   no shutdown  
   !
    // ทำซ้ำสำหรับ Port อื่นๆ และ VLAN 20 บนทั้ง SW1 และ SW2
   ```
   🌨️ กำหนดเกล็ดหิมะแต่ละเกล็ดให้อยู่ในก้อนที่ถูกต้อง!


4. **กำหนดค่า Trunk Port (บน SW1 และ SW2 ที่เชื่อมต่อกับ Router):**
   ```cisco
   interface FastEthernet0/1 // Port ที่เชื่อมต่อกับ Router
   switchport mode trunk         // กำหนดโหมด Port เป็น Trunk mode
   switchport trunk encapsulation dot1q // กำหนด Encapsulation เป็น 802.1Q
   switchport trunk allowed vlan 10,20 // อนุญาตให้ VLAN 10 และ 20 ผ่าน Trunk Port
   no shutdown
   ```
    ❄️❄️❄️  สร้างเส้นทางเชื่อมระหว่างก้อนหิมะด้วย Trunk!


**การกำหนดค่า Router (R1) - ขึ้นอยู่กับ Router แต่ละรุ่น:**

* **Subinterface:** สร้าง Subinterface บน Interface ที่เชื่อมต่อกับ Switch และกำหนดค่า IP Address และ VLAN ID ให้กับแต่ละ Subinterface.  เช่น `interface GigabitEthernet0/0.10 encapsulation dot1Q 10 ip address 192.168.10.1 255.255.255.0`  และ `interface GigabitEthernet0/0.20 encapsulation dot1Q 20 ip address 192.168.20.1 255.255.255.0`


**ตรวจสอบการตั้งค่า:**

* `show vlan brief` บน Switch เพื่อดูข้อมูล VLAN
* `show interface trunk` บน Switch เพื่อดูข้อมูล Trunk Port
* `show ip interface brief` บน Router เพื่อดู IP Address ของ Subinterface


** 🎉 เสร็จสิ้น! 🎉**  ตอนนี้ PC ใน VLAN เดียวกันจะสื่อสารกันได้  ส่วน PC ใน VLAN ต่างกันจะต้องผ่าน Router เท่านั้น!  เหมือนเกล็ดหิมะที่รวมกันเป็นก้อนๆ  สวยงามและเป็นระเบียบ!  ❄️☃️🌨️  
