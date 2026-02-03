# DBeaver — คู่มือสอนการใช้งานสำหรับมือใหม่

เอกสารนี้อธิบายการใช้งาน **DBeaver** อย่างละเอียด อ่านแล้วเข้าใจง่าย เหมาะสำหรับผู้ที่เพิ่งเริ่มต้น

---

## สารบัญ

1. [DBeaver คืออะไร](#dbeaver-คืออะไร)
2. [การติดตั้ง DBeaver](#การติดตั้ง-dbeaver)
3. [ส่วนติดต่อผู้ใช้ (UI) พื้นฐาน](#ส่วนติดต่อผู้ใช้-ui-พื้นฐาน)
4. [การเชื่อมต่อฐานข้อมูล](#การเชื่อมต่อฐานข้อมูล)
5. [การเรียกดูข้อมูลในตาราง](#การเรียกดูข้อมูลในตาราง)
6. [การเขียนและรัน SQL](#การเขียนและรัน-sql)
7. [การแก้ไขข้อมูลในตาราง](#การแก้ไขข้อมูลในตาราง)
8. [การสร้าง/แก้ไขตารางและโครงสร้าง](#การสร้างแก้ไขตารางและโครงสร้าง)
9. [การ Export และ Import ข้อมูล](#การ-export-และ-import-ข้อมูล)
10. [การจัดการ Connection และโปรเจกต์](#การจัดการ-connection-และโปรเจกต์)
11. [คำสั่งลัดและเทคนิคที่ใช้บ่อย](#คำสั่งลัดและเทคนิคที่ใช้บ่อย)
12. [สรุปแนวทางสำหรับมือใหม่](#สรุปแนวทางสำหรับมือใหม่)

---

## DBeaver คืออะไร

**DBeaver** คือ **โปรแกรมจัดการฐานข้อมูล (Database Client)** แบบ Universal

- **Universal** = รองรับฐานข้อมูลหลายชนิด เช่น MySQL, PostgreSQL, SQLite, MariaDB, Oracle, SQL Server ฯลฯ
- ใช้ **เชื่อมต่อ (Connect)** กับฐานข้อมูล แล้ว **ดู/แก้ไขข้อมูล**, **รัน SQL**, **Export/Import** ได้จากโปรแกรมเดียว
- มีทั้งแบบ **Community (ฟรี)** และแบบเสียเงิน รองรับฟีเจอร์ขั้นสูง

เหมาะกับ: นักพัฒนา, DBA, คนที่ต้องดู/แก้ข้อมูลใน DB, คนที่เขียน SQL บ่อย

---

## การติดตั้ง DBeaver

### ดาวน์โหลดและติดตั้ง

- ไปที่ [dbeaver.io/download](https://dbeaver.io/download/)
- เลือก **DBeaver Community** (ฟรี) แล้วดาวน์โหลดตามระบบปฏิบัติการ
- **Windows:** ติดตั้งจากไฟล์ `.exe`
- **macOS:** เปิดไฟล์ `.dmg` แล้วลาก DBeaver ไปที่ Applications
- **Linux:** ใช้ package manager หรือดาวน์โหลดไฟล์ติดตั้งตามที่เว็บแนะนำ

### เปิดโปรแกรมครั้งแรก

- ครั้งแรกอาจถามให้สร้าง **Workspace** (โฟลเดอร์เก็บการตั้งค่าและโปรเจกต์) ใช้ค่าตั้งต้นได้
- ถามให้ติดตั้ง **Driver** ของฐานข้อมูลเมื่อมีการเชื่อมต่อครั้งแรก — กด **Download** ได้เลย

---

## ส่วนติดต่อผู้ใช้ (UI) พื้นฐาน

เมื่อเปิด DBeaver จะเห็นพื้นที่หลักประมาณนี้:

| ส่วน | ความหมายสั้นๆ |
|------|----------------|
| **Database Navigator (ซ้าย)** | แสดง Connection ทั้งหมด, ฐานข้อมูล, ตาราง, View, ฯลฯ ใช้คลิกเพื่อเปิด/ขยายโหนด |
| **Editor / SQL Editor (กลาง)** | พื้นที่เขียน SQL และดูผลลัพธ์ (แท็บแบบ Query) |
| **Properties / Data (ขวาหรือล่าง)** | แสดงคุณสมบัติของ object ที่เลือก หรือแสดงข้อมูลในตาราง (Data tab) |
| **Script / Output (ล่าง)** | แสดง log, ผลการรัน script, ข้อความ error |

### การเปิด SQL Editor

- คลิกขวาที่ Connection หรือ Database หรือ Table → **SQL Editor** → **New SQL Script**
- หรือกด **Ctrl+U** (Windows/Linux) / **Cmd+U** (macOS)

### การดูข้อมูลในตาราง (Data)

- ขยาย Connection → Database → **Tables**
- **ดับเบิลคลิก** ที่ชื่อตาราง จะเปิดแท็บ **Data** แสดงข้อมูลในตาราง
- หรือคลิกขวาตาราง → **View Data**

---

## การเชื่อมต่อฐานข้อมูล

### สร้าง Connection ใหม่

1. คลิกไอคอน **New Database Connection** (ปลั๊กกับเครื่องหมายบวก) ที่แถบซ้าย หรือ **Database** → **New Database Connection**
2. เลือกชนิดฐานข้อมูล (เช่น **MySQL**, **PostgreSQL**, **SQLite**)
3. กรอกข้อมูลเชื่อมต่อตามชนิด DB

### ตัวอย่าง: MySQL / MariaDB

| ช่อง | ความหมาย | ตัวอย่าง |
|------|-----------|-----------|
| **Host** | ที่อยู่เซิร์ฟเวอร์ DB | `localhost` หรือ `127.0.0.1` |
| **Port** | พอร์ต | `3306` (ค่าเริ่มต้น MySQL) |
| **Database** | ชื่อฐานข้อมูล | `my_app` |
| **Username** | ชื่อผู้ใช้ | `root` |
| **Password** | รหัสผ่าน | (ใส่รหัสที่ตั้งไว้) |

- กด **Test Connection** เพื่อตรวจว่าเชื่อมต่อได้
- ถ้าโปรแกรมถามให้ดาวน์โหลด Driver ให้กด **Download** แล้วลอง Test อีกครั้ง
- กด **Finish** เพื่อบันทึก Connection

### ตัวอย่าง: SQLite

- เลือก **SQLite**
- ในช่อง **Path** เลือกไฟล์ `.sqlite` หรือ `.db` ในเครื่อง
- ไม่ต้องใส่ Username/Password
- กด **Test Connection** แล้ว **Finish**

### เปิด/ปิดการเชื่อมต่อ

- **เปิด:** คลิกขวาที่ Connection → **Connect** หรือดับเบิลคลิกที่ Connection
- **ปิด:** คลิกขวาที่ Connection → **Disconnect**
- สี/ไอคอนที่ Connection จะบอกสถานะ (เชื่อมต่ออยู่ หรือตัดการเชื่อมต่อแล้ว)

---

## การเรียกดูข้อมูลในตาราง

### ดูข้อมูล (Data)

1. ขยาย Connection → ขยาย **Databases** → ขยายชื่อ Database → ขยาย **Tables**
2. **ดับเบิลคลิก** ที่ชื่อตาราง
3. จะเปิดแท็บ **Data** แสดงแถวทั้งหมดในตาราง (หรือส่วนหนึ่ง ถ้ามีการแบ่งหน้า)

### การใช้งานในแท็บ Data

| การกระทำ | วิธีทำ |
|----------|--------|
| **เรียงคอลัมน์** | คลิกที่หัวคอลัมน์เพื่อเรียง (คลิกอีกครั้งสลับ ASC/DESC) |
| **กรอง (Filter)** | ใช้ช่อง Filter ด้านบน หรือคลิกขวาที่หัวคอลัมน์ → Filter |
| **รีเฟรช** | กด **F5** หรือไอคอน Refresh ที่แท็บ Data |
| **จำกัดจำนวนแถว** | ตั้งค่าในแถบด้านล่าง (เช่น 200 rows) |

### ดูโครงสร้างตาราง (Structure)

- คลิกขวาที่ตาราง → **View Table** หรือเลือกแท็บ **Structure** / **DDL**
- จะเห็นคอลัมน์ (Column), ชนิดข้อมูล (Type), Primary Key, Index ฯลฯ

---

## การเขียนและรัน SQL

### เปิด SQL Editor

- คลิกขวาที่ **Connection** หรือ **Database** → **SQL Editor** → **New SQL Script**
- หรือกด **Ctrl+U** (Windows/Linux) / **Cmd+U** (macOS)

### เขียนและรันคำสั่ง

1. พิมพ์คำสั่ง SQL ใน Editor เช่น:

```sql
SELECT * FROM users LIMIT 10;
```

2. **รันทั้งหมด:** กด **Ctrl+Enter** (Windows/Linux) หรือ **Cmd+Enter** (macOS)  
   **รันเฉพาะที่เลือก:** เลือกข้อความ SQL แล้วกด **Ctrl+Enter** / **Cmd+Enter**

3. ผลลัพธ์จะแสดงด้านล่างในรูปแบบตาราง

### คำสั่ง SQL พื้นฐานที่ใช้บ่อย

```sql
-- ดูข้อมูล
SELECT * FROM ชื่อตาราง LIMIT 100;

-- ดูเฉพาะคอลัมน์
SELECT id, name, email FROM users;

-- กรองด้วยเงื่อนไข
SELECT * FROM users WHERE status = 'active';

-- เรียง
SELECT * FROM products ORDER BY created_at DESC;

-- นับ
SELECT COUNT(*) FROM orders;
```

### การใช้หลายคำสั่งในไฟล์เดียว

- แยกคำสั่งด้วย `;`
- ถ้ารัน **Ctrl+Enter** โดยไม่เลือกข้อความ จะรันคำสั่งที่ cursor อยู่หรือคำสั่งที่เลือก
- สามารถเลือกเฉพาะบางบรรทัดแล้วรันได้

---

## การแก้ไขข้อมูลในตาราง

### แก้ไขผ่านแท็บ Data

1. เปิดตารางในแท็บ **Data** (ดับเบิลคลิกที่ตาราง)
2. คลิกที่เซลล์ที่ต้องการแก้ แล้วพิมพ์ค่าใหม่
3. กด **Ctrl+S** (Windows/Linux) หรือ **Cmd+S** (macOS) เพื่อ **Commit** (บันทึกการเปลี่ยนแปลง)
4. ถ้าไม่ต้องการบันทึก: คลิกขวาในพื้นที่ข้อมูล → **Cancel** หรือปิดแท็บแล้วเลือกไม่บันทึก

### ใส่แถวใหม่

- ในแท็บ Data กด **Ctrl+Shift+Insert** หรือคลิกไอคอน **Add row** (แถวใหม่จะปรากฏด้านล่าง)
- กรอกค่าในแต่ละคอลัมน์ แล้วกด **Ctrl+S** / **Cmd+S** เพื่อ Commit

### ลบแถว

- เลือกแถวที่ต้องการลบ (คลิกที่หมายเลขแถวด้านซ้าย)
- กด **Delete** หรือคลิกขวา → **Delete Row**
- กด **Ctrl+S** / **Cmd+S** เพื่อ Commit

### หมายเหตุ

- การแก้ไข/เพิ่ม/ลบจะส่งคำสั่ง **UPDATE / INSERT / DELETE** ไปที่ฐานข้อมูลเมื่อ Commit
- ถ้าตารางมีข้อจำกัด (Constraint) หรือ Trigger อาจมี error ได้ — อ่านข้อความใน Script/Output

---

## การสร้าง/แก้ไขตารางและโครงสร้าง

### สร้างตารางใหม่ (ด้วย SQL)

ใน SQL Editor:

```sql
CREATE TABLE products (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    price DECIMAL(10, 2),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

จากนั้นรันด้วย **Ctrl+Enter** / **Cmd+Enter** แล้ว Refresh ที่โหนด Tables (F5)

### สร้างตารางผ่าน UI (แบบกราฟิก)

1. คลิกขวาที่ **Tables** ภายใต้ Database ที่ต้องการ → **Create** → **Table**
2. ตั้งชื่อตาราง แล้วเพิ่มคอลัมน์ (ชื่อ, ชนิดข้อมูล, Nullable, Default ฯลฯ)
3. กำหนด Primary Key ถ้าต้องการ
4. กด **Save** / **Apply**

### แก้ไขโครงสร้างตาราง (Alter)

- คลิกขวาที่ตาราง → **Edit Table**
- แก้ไขคอลัมน์ (เพิ่ม/ลบ/เปลี่ยนชนิด) แล้ว Save

หรือใช้ SQL:

```sql
ALTER TABLE products ADD COLUMN description TEXT;
ALTER TABLE products MODIFY COLUMN name VARCHAR(500);
```

---

## การ Export และ Import ข้อมูล

### Export ข้อมูล

1. เปิดตารางในแท็บ **Data** หรือรัน SELECT แล้วได้ผลลัพธ์
2. คลิกขวาที่ผลลัพธ์หรือที่ตาราง → **Export Data** หรือใช้เมนู **Tools** → **Export Data**
3. เลือกรูปแบบ เช่น **CSV**, **SQL (INSERT)**, **JSON**, **Excel**
4. กำหนดเส้นทางไฟล์และตัวเลือก (เช่น delimiter ของ CSV) แล้วกด **Finish**

### Import ข้อมูล

1. คลิกขวาที่ตารางปลายทาง → **Import Data** หรือ **Tools** → **Import Data**
2. เลือกไฟล์ต้นทาง (CSV, SQL ฯลฯ)
3. กำหนดการแมปคอลัมน์ (column mapping) ถ้าจำเป็น
4. กด **Proceed** / **Finish** เพื่อนำข้อมูลเข้า

### Export Connection (สำรองการตั้งค่า)

- คลิกขวาที่ Connection → **Export Connection** จะได้ไฟล์เก็บการตั้งค่า (ใช้ย้ายเครื่องหรือแบ่งกันใช้ได้)

---

## การจัดการ Connection และโปรเจกต์

### จัดการ Connection

| การกระทำ | วิธีทำ |
|----------|--------|
| **แก้ไข Connection** | คลิกขวาที่ Connection → **Edit Connection** |
| **ลบ Connection** | คลิกขวาที่ Connection → **Delete** |
| **Duplicate Connection** | คลิกขวาที่ Connection → **Duplicate** (ใช้สร้าง Connection ใหม่โดยใช้การตั้งค่าเดิมเป็นฐาน) |

### โปรเจกต์ (Project)

- DBeaver แบ่งงานเป็น **Project** ได้ (เช่น Project A, Project B)
- แต่ละ Project มี Connection, Script, Query ได้แยกกัน
- สร้าง Project: **Project** → **New Project** หรือใช้ Project เริ่มต้นก็ได้
- เปลี่ยน Project: ใช้เมนูหรือรายการ Project ด้านซ้าย

### บันทึก Script / Query

- เขียน SQL ใน SQL Editor แล้ว **Save** (Ctrl+S / Cmd+S) เก็บเป็นไฟล์ `.sql` ในโปรเจกต์หรือโฟลเดอร์ที่กำหนด
- เปิดไฟล์เดิม: **File** → **Open** หรือลากไฟล์ `.sql` ลงใน DBeaver

---

## คำสั่งลัดและเทคนิคที่ใช้บ่อย

| การกระทำ | Windows/Linux | macOS |
|----------|----------------|--------|
| เปิด SQL Editor ใหม่ | Ctrl+U | Cmd+U |
| รัน SQL | Ctrl+Enter | Cmd+Enter |
| รัน SQL (ทั้งหมดในสคริปต์) | Ctrl+Alt+Enter | Cmd+Alt+Enter |
| รีเฟรช (Refresh) | F5 | F5 |
| บันทึก (Save) | Ctrl+S | Cmd+S |
| Auto-complete ใน SQL | Ctrl+Space | Cmd+Space |
| แสดงโครงสร้างตาราง (DDL) | คลิกขวาตาราง → View DDL | เหมือนกัน |

### เทคนิคที่ใช้บ่อย

- **ลากตารางลง SQL Editor:** ลากชื่อตารางจาก Database Navigator ลงใน SQL Editor จะได้ `SELECT * FROM ชื่อตาราง` อัตโนมัติ
- **ดูข้อมูลตัวอย่าง:** คลิกขวาตาราง → **View Data** หรือดับเบิลคลิก
- **กรองใน Data view:** ใช้ช่อง Filter ด้านบนหรือคลิกขวาที่หัวคอลัมน์ → Filter
- **ตรวจสอบ Connection ที่ใช้:** ดูที่มุมของ SQL Editor ว่าอยู่ภายใต้ Connection ไหน (เลือกได้ถ้ามีหลาย Connection)

---

## สรุปแนวทางสำหรับมือใหม่

1. **ติดตั้ง DBeaver** แล้วเปิดโปรแกรม สร้าง Workspace ตามที่แนะนำ
2. **สร้าง Connection** ตามชนิดฐานข้อมูล (MySQL, PostgreSQL, SQLite ฯลฯ) ให้กรอก Host, Port, Database, Username, Password ให้ถูก แล้วกด Test Connection
3. **ดูข้อมูล:** ขยาย Connection → Database → Tables แล้วดับเบิลคลิกที่ตารางเพื่อเปิดแท็บ Data
4. **เขียน SQL:** คลิกขวาที่ Connection หรือ Database → SQL Editor → New SQL Script แล้วพิมพ์คำสั่ง จากนั้นกด Ctrl+Enter / Cmd+Enter เพื่อรัน
5. **แก้ไขข้อมูล:** แก้ในแท็บ Data ได้เลย แล้วกด Ctrl+S / Cmd+S เพื่อ Commit
6. **Export/Import:** ใช้คลิกขวาที่ตารางหรือผลลัพธ์ → Export Data / Import Data
7. **จำคำสั่งลัด:** Ctrl+Enter (รัน SQL), F5 (Refresh), Ctrl+U (SQL Editor ใหม่)
8. **มี error:** ดูที่แท็บ Script/Output ด้านล่าง จะมีข้อความ error จาก DB แจ้งให้แก้ไข

ถ้าทำตามขั้นตอนนี้และลองเชื่อมต่อ DB จริงสักหนึ่งตัว แล้วลอง SELECT / ดู Data / Export จะเริ่มคุ้นกับ DBeaver ได้เร็ว

---

*คู่มือนี้เขียนสำหรับมือใหม่ อ่านแล้วเข้าใจง่าย และสามารถนำไปปฏิบัติตามได้ทันที*
