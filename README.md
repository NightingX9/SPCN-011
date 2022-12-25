# SPCN-011
**สร้าง vm and ct on Proxmox cluster**
# create master vm (ubuntu-22.04)
1.เลือก Creat Virtual Machine

2.กรอกรายละเอียดชื่อและตั้งค่าต่างๆ

      -ตัวอักษรชื่อภาษาอังกฤษตัวเอง  3 ตัว - เลข VM ID                                                                              
      -ช่อง Resource Pool เลือก Special_CN
      -ช่อง ISO image เลือก ubuntu-22.04.1-live-server-amd64
      -System ตั้งค่าตามค่า default 
      -Disk ตั้งค่าตามค่า default 
      -CPU ตั้งค่าตามค่า default
      -Memory เลือกค่า 2048
      -Netwoek ตั้งค่าตามค่า default
      
![image](https://user-images.githubusercontent.com/118722718/209476270-484e8603-c0f6-4aa2-866f-a88b3b860189.PNG)


3.Install ตามขั้นตอน และจะมีให้กรอกข้อมูล

4.ตั้งค่า SSH เลือก Github ใส่รายละเอียด Username Github Confirm SSH Keys แล้วรอติดตั้ง

**Setup timezone**

 -ใช้คำสั่ง เพื่อตั้งค่าเวลา
 
     Sudo timedatectl set-timezone Asia/Bankok
		 
 -ใช้คำสั่ง เพื่อเช็คเวลา
 
     date
     
 **ติดตั้ง QEMU Guest Agent**
 -Shutdown VM ไปแถบ Option ของ VM ตัวนั้น เลือกกด QEMU Guest Agent ปรับเป็น Enable
 ![image](https://user-images.githubusercontent.com/118722718/209476557-436b79c6-3b95-48f3-b368-dc74014e7beb.PNG)
 
 -ใช้คำสั่ง

 sudo apt install qemu-guest-agent
 
 sudo systemctl start qemu-guest-agent
-ใช้คำสั่งนี้เพื่อตรวจสอบสถานะการทำงานของ QEMU Guest Agent

 sudo systemctl status qemu-guest-agent
 
 ![image](https://user-images.githubusercontent.com/118722718/209476598-ac64b5bd-f29b-4059-98e3-2fcc77418cb1.PNG)
 
 -หน้า Summary จะมีเลข IPs เพิ่มมาหลังจากทำการเปิดใช้ QEMU Guest Agent
 
 -ปิดเครื่อง และกด More เลือก Convert to template

![image](https://user-images.githubusercontent.com/118722718/209476807-cdb272ac-17f1-4478-94c0-d53fbb9c97aa.PNG)

-clone from template สร้าง vm ใหม่จำนวน 2 vm

![image](https://user-images.githubusercontent.com/118722718/209476988-b83245d3-a9e4-40da-bf9d-f9c545e9f6f7.PNG)

-change hostname สำหรับ vm ใหม่

sudo hostnamectl hostname *ชื่ออะไรก็ได้*
-กดเลือกเครื่อง clone แล้วเปลี่ยน IP โดยใช้คำสั่ง

sudo -i
rm /var/lib/dbus/machine-id
nano /etc/machine-id 
ln -s /etc/machine-id /var/lib/dbus/machine-id
-Restart os

-เครื่อง Clone 1
![image](https://user-images.githubusercontent.com/118722718/209477050-816a9333-2c7e-4e5e-8ff6-964840220475.PNG)

-เครื่อง Clone 2
![image](https://user-images.githubusercontent.com/118722718/209477098-5129090a-1db6-486b-bd23-c3e8209a08cd.PNG)

# create create container template

-กดเลือกปุ่ม Create CT

-Create LXC Container หน้า General ใส่รายละเอียดข้อมูล แล้ว next เลือกค่า default

-Create LXC Container หน้า Network เลือก IPv4 เป็น DHCP และ IPv6 เป็น SLAAC

-หน้า Summary

![image](https://user-images.githubusercontent.com/118722718/209477226-e8243d7a-7092-4262-b23f-63246cc3ed12.PNG)

