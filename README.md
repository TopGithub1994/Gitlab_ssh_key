# Gitlab_SSH_Key
##ขั้นตอนในภาพรวม
- ตรวจสอบว่าเรามี SSH client หรือยัง
- สร้าง SSH key สำหรับ git hosting แต่ละเจ้าแยกกัน
- สร้าง key แล้ว เพิ่ม key เข้าไปใน ssh-agent
- นำ public key (ไฟล์ .pub) ไปใส่ใน git hosting
### 1. ตรวจสอบ SSH client
~~~
ssh -V
~~~
### 2. สร้าง SSH key
~~~
cd ~/.ssh
~~~
~~~
ssh-keygen -t rsa -b 2048 -C "your_email+github@gmail.com"
~~~
-C option นี้คือ comment เราจะใส่ email address อันที่ลงทะเบียนกับ git hosting เจ้านั้นๆ -b จำนวน bits ที่จะใช้ในการสร้าง key สำหรับแบบ rsa ใช้ 2048 ถือว่าเพียงพอแล้ว -t เราจะใช้ key encrytion แบบ rsa
กด Enter แล้วจะเจอคำถาม
~~~
Enter a file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]
~~~
ให้เปลี่ยนชื่อไฟล์ก่อนจะกด Enter เช่น ผมจะเปลี่ยนเป็น id_rsa_github สำหรับสร้าง key ของ github

ต่อไป แนะนำให้ใส่ passphrase หรือ password สำหรับ key ที่กำลังจะสร้างด้วย ถือเป็นอีกด่านนึง หาก key หลุดออกไปสู่สาธารณะ จะต้องรู้ password ด้วย ถ้าไม่อยากใส่ passpharse ก็ Enter ข้ามไปเฉยๆ
~~~
Enter passphrase (empty for no passphrase): [Type a passphrase]
Enter same passphrase again: [Type passphrase again]
~~~
หลังจากใส่ passpharse แล้ว เราจะได้ผลคล้ายแบบนี้
~~~
Your identification has been saved in id_rsa_github.
Your public key has been saved in id_rsa_github.pub.
The key fingerprint is:
SHA256:****7Ts7ALeuST60fODcLweRT3N1gqtYN8UaLri1eh4 d***+github@gmail.com
The key's randomart image is:
+---[RSA 2048]----+
|             o   |
|         . .o + o|
|        ...o.= o.|
|       oo B.O .  |
|        SB X.+   |
|       oB.*.oo   |
|        +*.+o.   |
+----[SHA256]-----+
~~~
อันนี้ถือว่าเสร็จการสร้าง key สำหรับ git hosting 1 เจ้า สำหรับเจ้าต่อๆไป ผมก็จะเปลี่ยน comment -C ตรง command line ให้ตรงกับ email ที่ใช้ register กับ hosting นั้นๆ
### 3. Add key to gitlab
#### 1. Copy the contents of your public key file. You can do this manually or use a script. For example, to copy an ED25519 key to the clipboard:
~~~
cat ~/.ssh/id_ed25519.pub | clip
~~~

#### 2. Sign in to GitLab.
#### 3. In the top right corner, select your avatar.
#### 4. Select >Preferences.
#### 5. From the left sidebar, select SSH Keys.
#### 6. In the Key box, paste the contents of your public key. If you manually copied the key, make sure you copy the entire key, which starts with **ssh-ed25519** or **ssh-rsa**, and may end with a comment.
#### 7. In the Title text box, type a description, like Work Laptop or Home Workstation.
#### 8. Select Add key.
