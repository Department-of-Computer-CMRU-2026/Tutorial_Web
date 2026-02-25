# คู่มือการใช้งาน GitHub

## GitHub คืออะไร

**GitHub** เป็นแพลตฟอร์มที่ใช้เก็บและจัดการโค้ด (repository) ด้วยระบบ **Git** เมื่อทำงานคนเดียว GitHub ช่วยให้คุณ:

- เก็บประวัติการเปลี่ยนแปลงของโค้ด (version control) — ย้อนดูหรือกลับไปเวอร์ชันเก่าได้
- เก็บโค้ดไว้บนคลาวด์ — ไม่ต้องพึ่งแค่เครื่องเดียว
- เปิดเผยโปรเจกต์เป็น Public หรือเก็บเป็น Private ได้ตามต้องการ

---

## การติดตั้งและตั้งค่า

### 1. สร้างบัญชี GitHub

1. ไปที่ [github.com](https://github.com)
2. กด **Sign up** แล้วกรอกอีเมล รหัสผ่าน และชื่อผู้ใช้
3. ยืนยันอีเมลตามที่ระบบส่งมา

### 2. ติดตั้ง Git บนเครื่อง

- **Windows:** ดาวน์โหลดจาก [git-scm.com](https://git-scm.com) แล้วติดตั้ง
- **macOS:** เปิด Terminal แล้วรัน `xcode-select --install` หรือติดตั้งผ่าน Homebrew: `brew install git`
- **Linux:** ใช้คำสั่งของ package manager เช่น `sudo apt install git` (Ubuntu/Debian)

ตรวจสอบว่าติดตั้งสำเร็จ:

```bash
git --version
```

### 3. ตั้งค่าชื่อและอีเมล (ครั้งแรกเท่านั้น)

```bash
git config --global user.name "ชื่อของคุณ"
git config --global user.email "your.email@example.com"
```

อีเมลควรตรงกับอีเมลที่ใช้สมัคร GitHub

### 4. เชื่อมต่อกับ GitHub ด้วย SSH (แนะนำ)

1. สร้างคีย์ SSH:

```bash
ssh-keygen -t ed25519 -C "your.email@example.com"
```

กด Enter เพื่อใช้ path เริ่มต้น และตั้งรหัสผ่าน (หรือเว้นว่างได้)

2. เปิด SSH agent แล้วเพิ่มคีย์:

```bash
# Windows (PowerShell)
Get-Service ssh-agent | Set-Service -StartupType Manual
Start-Service ssh-agent
ssh-add $env:USERPROFILE\.ssh\id_ed25519

# macOS / Linux
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

3. คัดลอกคีย์สาธารณะไปใส่ใน GitHub:
   - ไปที่ **GitHub → Settings → SSH and GPG keys → New SSH key**
   - วางเนื้อหาจากไฟล์ `~/.ssh/id_ed25519.pub` (หรือ `id_rsa.pub` ถ้าใช้ RSA)

ทดสอบการเชื่อมต่อ:

```bash
ssh -T git@github.com
```

ถ้าขึ้นว่า "Hi username! You've successfully authenticated..." แสดงว่าพร้อมใช้แล้ว

---

## การทำงานพื้นฐาน

### สร้าง Repository ใหม่บน GitHub

1. กด **+** มุมขวาบน → **New repository**
2. ตั้งชื่อ repo (เช่น `my-project`)
3. เลือก Public หรือ Private
4. (ไม่จำเป็น) เลือก **Add a README file** ถ้าอยากให้มี README ตั้งแต่แรก
5. กด **Create repository**

### นำโปรเจกต์ที่มีอยู่ขึ้น GitHub

ถ้ามีโฟลเดอร์โปรเจกต์อยู่แล้วบนเครื่อง:

```bash
cd path/to/your-project
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin git@github.com:USERNAME/REPO-NAME.git
git push -u origin main
```

แทนที่ `USERNAME` และ `REPO-NAME` ด้วยชื่อผู้ใช้และชื่อ repo จริง

### Clone โปรเจกต์จาก GitHub มาไว้ที่เครื่อง

```bash
git clone git@github.com:USERNAME/REPO-NAME.git
cd REPO-NAME
```

หรือใช้ HTTPS:

```bash
git clone https://github.com/USERNAME/REPO-NAME.git
```

### ขั้นตอนการแก้ไขและส่งโค้ด (Workflow ปกติ)

1. **ดึงโค้ดล่าสุดจาก GitHub**

```bash
git pull origin main
```

2. **แก้ไขไฟล์** ตามที่ต้องการ (เขียนโค้ด แก้ README ฯลฯ)

3. **ดูสถานะการเปลี่ยนแปลง**

```bash
git status
```

4. **เพิ่มไฟล์ที่ต้องการส่งขึ้น GitHub**

```bash
# เพิ่มทีละไฟล์
git add filename.txt

# เพิ่มทุกไฟล์ที่เปลี่ยน
git add .

# เพิ่มเฉพาะไฟล์ที่ตรง pattern
git add src/*.js
```

5. **สร้าง Commit (บันทึกจุดหนึ่งของประวัติ)**

```bash
git commit -m "อธิบายสั้นๆ ว่าแก้อะไร หรือเพิ่มฟีเจอร์อะไร"
```

ข้อความ commit ควรสั้น ตรงประเด็น และเป็นปัจจุบัน (present tense) เช่น "Add login form" หรือ "Fix navbar on mobile"

6. **ส่งโค้ดขึ้น GitHub**

```bash
git push origin main
```

ถ้าตั้ง `-u origin main` ไว้แล้ว สามารถใช้แค่:

```bash
git push
```

### ดูประวัติ Commit

```bash
git log
```

กด `q` เพื่อออกจากมุมมอง log

ดูแบบย่อหนึ่งบรรทัดต่อ commit:

```bash
git log --oneline
```

---

## คำสั่ง Git ที่ใช้บ่อย

| คำสั่ง | ความหมาย |
|--------|-----------|
| `git status` | ดูว่าไฟล์ไหนถูกแก้/เพิ่ม/ยังไม่ add |
| `git add .` | เพิ่มการเปลี่ยนแปลงทั้งหมดเข้า staging |
| `git commit -m "ข้อความ"` | สร้าง commit พร้อมข้อความ |
| `git push` | ส่ง commit ขึ้น remote (เช่น GitHub) |
| `git pull` | ดึงและรวมโค้ดล่าสุดจาก remote |
| `git clone URL` | โหลด repo จาก GitHub มาไว้ที่เครื่อง |

---

## แนวทางปฏิบัติที่ดี

1. **Commit บ่อย แต่ละ commit ควรเป็นหน่วยงานเดียว**  
   เช่น แก้บั๊กหนึ่งจุด หรือเพิ่มฟีเจอร์หนึ่งอย่าง

2. **เขียน commit message ให้เข้าใจได้**  
   ใช้ present tense และอธิบายว่า “ทำอะไร” ไม่ใช่ “ทำไปแล้ว”

3. **ดึงโค้ดก่อน push (ถ้าใช้หลายเครื่อง)**  
   ถ้าแก้โค้ดจากเครื่องอื่นหรือจากเว็บ GitHub แล้ว ควรรัน `git pull origin main` ก่อน `git push` เพื่อลด conflict

5. **เขียน README และ .gitignore**  
   README อธิบายวิธีรันโปรเจกต์; .gitignore กันไม่ให้ส่งไฟล์ที่ไม่จำเป็น (เช่น `node_modules`, `.env`) ขึ้น GitHub

6. **อย่า commit ข้อมูลลับ**  
   ไม่ใส่รหัสผ่าน, API key หรือ token ในโค้ดที่ push ขึ้น GitHub ใช้ตัวแปรสภาพแวดล้อมหรือ secret management แทน

---

## ลิงก์ที่เป็นประโยชน์

- [เอกสาร Git (อย่างเป็นทางการ)](https://git-scm.com/doc)
- [GitHub Docs](https://docs.github.com)
- [GitHub Learning Lab](https://skills.github.com/) — ฝึกใช้ Git และ GitHub แบบมีแบบฝึกหัด

---
