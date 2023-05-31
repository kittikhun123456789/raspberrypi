# **Command Line พื้นฐานบน Ubuntu**


## 1. การจัดการ Folder และ File

- สร้าง folder on ubuntu

    ```
    $mkdir {folder name}
    ```
    
- เปลี่ยนชื่อ folder หรือ file

    ```
    $mv {folder เดิม} {folder ใหม่}
    ```

- ลบ folder or file

    ```
    $rmdir {folder name}
    $rm -rf {folder name}
    $rm {FileName.py}
    ```
- เช็ค path ของ folder ที่กาลังดาเนินการอยู่ตาแหน่งปัจจุบัน

    ```
    $pwd
    ```
- สร้าง .py file

    ```
    $nano {FileName.py}
    ```

- Running .py file

    ```
    $python {FileName.py}
    ```

- เปิด file แบบไม่แก้ไข

    ```
    $cat {FileName.py}
    ```

- เปิด file แบบแก้ไข

    ```
    $vi {FileName.py}
    #กด i เพื่อแก้ไข
    #กด esc + : wq (save)
    #กด esc + : q! (save)

    $nano {FileName.py}
    #กด ctrl s (save)
    #กด ctrl x (ปิดไฟล์)
    ```
- ย้ายไฟล์ on Could

    ```
    #ย้ำย test.py ที่ directory ปัจจุบัน ไปที่ folder ชื่อ code
    $mv test.py code

    #ย้ำย main.c def.h ไปที่ path: /home/usr/rapid/
    $mv main.c def.h /home/usr/rapid/

    #ย้ำย file.c ทั้งหมด ที่ directory ปัจจุบัน ไปที่ folder ชื่อ code
    $mv *.py code
    ```

- ย้ายไฟล์ที่อยู่บน Could to PC 

    ```
   $cd /mnt/d/Master-Degree/Year1Term2/AIPrototype/ubuntu/AIprototype65/
   $scp uesrname@12.34.567.89:/home/code/test.py .
   $scp –T uesrname@12.34.567.89:"'/home/code/test 02.py '" . #กรณีชื่อไฟล์มีวรรค
    ```

- ย้ายไฟล์ PC to could

  ```
  $scp /mnt/d/Master-Degree/Year1Term2/AIPrototype/ubuntu/AIprototype65/code/test.py uesrname@12.34.567.89:/home/code
  ```

---

## 2. การเปิดใช้งาน jupyter notebook ##

- สร้ำง Virtual Environment with Anaconda

    ```
    #สร้าง Environment โดยตั้งชื่อตามตนเอง (MyEnv)
    $conda create -n MyEnv
    $conda activate MyEnv

    ##ออกจาก Environment นั้น
    $deactivate MyEnv 
    $conda activate base 

    #เช็ค Environment ที่มีอยู่
    $conda env list

    #ลบ Environment
    $conda env remove -n MyEnv
    ```

- Add Virtual Environment to Jupyter Notebook

    ```
    #ติดตั้ง ipykernel ซึ่งให้เคอร์เนล IPython สาหรับ Jupyter
    $pip install --user ipykernel #Install ipython

    #เพิ่ม virtual environment to Jupyter 
    ##เปิดไฟล์ kernel.json เพื่อเช็ค local
    $python -m ipykernel install --user --name=MyEnv
    
    #คำสั่งอื่นๆ
    ##เช็ค kernelที่มีอยู่
    $jupyter kernelspec list 

    ##ลบ kernel ที่สร้าง
    $jupyter kernelspec uninstall MyEnv
    ```

- เปิด jupyter notebook ใน screen

    ```
    #สร้าง screen
    $screen –S jupy 

    #เช็ค screen ที่สร้ำงไว้หรือเข้า screen
    $screen –R
    $screen –R jupy 

    #เปิด jupyter notebook
    $conda activate MyEnv
    $jupyter notebook

    ##เข้ำไปในโฟล์เดอร์ที่ต้องการเปิดแล้วจะแสดง Link localhost จากนั้นเปิด port ด้วยคำสั่ง -L เพื่อให้เข้าใช้งาน jupyter notebook ได้ 
    ##ตัวอย้างเลข port เช่น 8000, 8888, 8889, 8890 

    #login เข้า could azure ใหม่ด้วยคำสั่ง
    $ssh -L 8000:localhost:8888 usernsme@12.34.567.89
    ```

---

## 3. การใช้งาน GitHub ##

- Install Git สาหรับใช้งาน Git ครั้งแรก

    ```
    #install บนเครื่อง ubuntu 
    $sudo apt install git  

    #install เฉพาะ Env. ที่ใช้
    $conda activate MyEnv
    $conda install git

    $git config --global user.name "WiratchawaKannika"  #user name ที่ใช้บน GitHub
    $git config --global user.email "kannikaw@kkumail.com" #Email ที่ใช้บน GitHub
    ``` 

- การ copy/clone โปรเจคจำลองจากโปรเจคหลักโดยที่เปลี่ยนแปลงไฟล์แล้วจะไม่กระทบกับโปรเจคหลัก 

    ```
    $git clone https://github.com/WiratchawaKannika/AIprototype65.git #HTTPS link
    ```

- คำสั่ง git พื้นฐานที่ต้องใช้บ่อย

    ```
    #ตรวจสอบว่าไฟล์ไหนที่มีการเปลี่ยนแปลงหรือไฟล์ที่ยังไม่ได้ add ยังไม่ถูกจัดการบ้าง
    $ git status

    #เพิ่มไฟล์เข้าไป stage (เป็นการระบุว่าต้องการที่จะสร้างความเปลี่ยนแปลงไฟล์ไหนใน git บ้าง)
    ##กรณีเพิ่มไฟล์เดียว test.py
    $git add test.py 

    ##กรณีต้องการเพิ่มไฟล์ทั้งหมดที่มีการเปลี่ยนแปลงทั้งโฟลเดอร์
    $git add *      

    ##กรณีต้องการเพิ่มทั้งโฟลเดอร์
    $git add . 

    #ยืนยันการเปลี่ยนแปลงไฟล์ลง stage และสามารถใส่ comment โดยเติม –m
    $git commit –m "first commit"

    #ส่งไฟล์ที่ commit สู่ remote repository
    $git push
    ```

- Update file ที่มีการเปลี่ยนแปลงบน remote repository (ต้องทำก่อนเปลี่ยนแปลงไฟล์/โฟลเดอร์ ใดๆ บน git เสมอ)

    ```
    git pull
    ```

---
## 4. การปรับความละเอียดหน้าจอ กับ raspi

    ```
    $xrandr {จะขึ้นมาให้เลือกความละเอียดหน้าจอ}
    ```
    
    ```
    $xrandr -s {ตามด้วยความละเอียดหน้าจอ}
    ```

