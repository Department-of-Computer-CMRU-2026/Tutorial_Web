# Laravel — คู่มือสอนการใช้งานสำหรับมือใหม่

## Laravel คืออะไร

**Laravel** คือ **PHP Framework** สำหรับพัฒนาเว็บแอปพลิเคชัน

- **Framework** = โครงและเครื่องมือที่ช่วยให้เขียนโค้ดเป็นระบบ ไม่ต้องเขียนทุกอย่างจากศูนย์
- ใช้ภาษา **PHP** เป็นหลัก
- มีระบบ **Routing**, **Controller**, **View**, **Model**, **Migration**, **Validation** ครบ
- มี **Artisan** เป็นเครื่องมือคำสั่งในเทอร์มินัลสำหรับสร้างไฟล์ รัน migration ฯลฯ

เหมาะกับ: เว็บแอป, API, แอดมิน, ระบบสมาชิก, E-commerce ฯลฯ

---

## การติดตั้ง Laravel

### สิ่งที่ต้องมีก่อนติดตั้ง

- **PHP** (แนะนำ 8.3 ขึ้นไป) และส่วนขยายที่ Laravel ต้องการ
- **Composer** — โปรแกรมจัดการ package ของ PHP
- (ถ้าใช้ฐานข้อมูล) **MySQL** หรือ **PostgreSQL** หรือ **SQLite**

ตรวจสอบ PHP และ Composer:

```bash
php -v
composer --version
```

### วิธีการสร้างโปรเจกต์แบบใหม่

#### ขั้นตอนที่ 1: สร้างโปรเจกต์

มีสองวิธีหลัก (อ้างอิงจาก [Laravel 12.x - Creating a Laravel Application](https://laravel.com/docs/12.x#creating-a-laravel-application)):

**วิธีที่ 1 — ใช้ Composer (ไม่ต้องติดตั้ง Laravel Installer)**

เปิด Terminal แล้วรัน:

```bash
composer create-project laravel/laravel ชื่อโปรเจกต์
```

**วิธีที่ 2 — ใช้ Laravel Installer (ต้องติดตั้งก่อน)**

ติดตั้ง Laravel Installer ครั้งเดียว:

```bash
composer global require laravel/installer
```

จากนั้นสร้างโปรเจกต์:

```bash
laravel new example-app
```

- Installer จะถามให้เลือก testing framework, database, และ starter kit ได้
- เมื่อเสร็จจะได้โฟลเดอร์โปรเจกต์ในตำแหน่งปัจจุบัน

#### ขั้นตอนที่ 2: เข้าไปในโฟลเดอร์โปรเจกต์

```bash
cd my-app
```

- `.env` เก็บค่าสภาพแวดล้อม (รหัส DB, APP_KEY ฯลฯ) — **อย่า commit ไฟล์นี้ขึ้น Git**

#### ขั้นตอนที่ 4: ตั้งค่าฐานข้อมูล (ถ้าใช้)

แก้ไขไฟล์ **`.env`** ให้ตรงกับเซิร์ฟเวอร์ฐานข้อมูลของคุณ เช่น:

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=root
DB_PASSWORD=
```

จากนั้นสร้างตาราง (ถ้ามี migration):

```bash
php artisan migrate
```

#### ขั้นตอนที่ 5: รันเซิร์ฟเวอร์พัฒนา

**แบบธรรมดา (เฉพาะ Laravel):**

```bash
#php artisan serve
```

**แบบรัน Frontend ด้วย (Vite + Laravel) — ตาม [Laravel 12.x](https://laravel.com/docs/12.x#creating-a-laravel-application):**

```bash
bun install && bun run build
#composer run dev
```

- `composer run dev` จะรันทั้ง PHP server และ Vite (ถ้าโปรเจกต์มี frontend)
- เปิดเบราว์เซอร์ที่ **http://127.0.0.1:8000** หรือ **http://localhost:8000** จะเห็นหน้า welcome ของ Laravel

---

## โครงสร้างโฟลเดอร์โปรเจกต์

เมื่อสร้างโปรเจกต์ Laravel จะได้โฟลเดอร์ประมาณนี้ (สรุปเฉพาะที่มือใหม่ควรรู้):

| โฟลเดอร์/ไฟล์ | ความหมายสั้นๆ |
|----------------|----------------|
| **app/** | โค้ดหลักของแอป — Controllers, Models, และคลาสอื่นๆ |
| **app/Http/Controllers/** | เก็บ **Controller** ทั้งหมด |
| **app/Models/** | เก็บ **Model** (ตัวแทนตารางในฐานข้อมูล) |
| **config/** | ไฟล์ตั้งค่า เช่น ฐานข้อมูล, session, mail |
| **database/migrations/** | ไฟล์ **Migration** สำหรับสร้าง/แก้ไขตาราง |
| **resources/views/** | ไฟล์ **View** (Blade template) หน้า HTML |
| **routes/** | กำหนด **Route** (URL ไปยัง Controller/Closure) |
| **routes/web.php** | Route สำหรับเว็บปกติ (ไม่ใช่ API) |
| **public/** | ไฟล์ที่เข้าถึงได้จาก URL โดยตรง (CSS, JS, รูป) |
| **.env** | ตัวแปรสภาพแวดล้อม (รหัส DB, APP_KEY ฯลฯ) — **ไม่ควร commit รหัสลับ** |

มือใหม่ควรโฟกัสที่: `routes/web.php` → `app/Http/Controllers` → `resources/views` → `app/Models` และ `database/migrations`

---

## การทำงานของ Laravel (Request → Response)

สรุปการทำงานของ Laravel + Livewire

1. ผู้ใช้เปิด URL: Laravel ดูใน routes ว่า URL นี้เชื่อมกับ Livewire Component ตัวไหน
2. Initial Load: Component ทำการ Render หน้า HTML ครั้งแรกส่งกลับไปให้เบราว์เซอร์ (เหมือน MVC ปกติ)
3. User Interaction: เมื่อผู้ใช้ทำบางอย่าง (เช่น คลิกปุ่ม wire:click) Livewire จะส่ง Request ไปที่เซิร์ฟเวอร์แบบเบื้องหลัง (AJAX)
4. Component ทำงาน: ตัว Class ของ Component (PHP) จะรัน Method หรืออัปเดตค่าตัวแปร (Properties) ตามที่สั่ง
5. Smart Response: Livewire ส่งเฉพาะ HTML ส่วนที่เปลี่ยนแปลงกลับไปอัปเดตบนหน้าจอให้ทันที โดยไม่ต้อง Refresh หน้าเว็บ

ดังนั้น สิ่งที่คุณต้องทำคือ กำหนด Route → สร้าง Component Class (เขียน Logic) → สร้าง Component View (ใช้คำสั่ง wire:)

---

## คำสั่ง Artisan ที่ใช้บ่อย

| คำสั่ง | ความหมาย |
|--------|-----------|
| `php artisan serve` | รันเซิร์ฟเวอร์พัฒนา |
| `php artisan make:controller ชื่อController` | สร้าง Controller |
| `php artisan make:model ชื่อModel` | สร้าง Model |
| `php artisan make:migration ชื่อ_migration` | สร้าง Migration |
| `php artisan migrate` | รัน migration (สร้าง/อัปเดตตาราง) |
| `php artisan migrate:rollback` | ย้อน migration ชุดล่าสุด |
| `php artisan make:model Product -m` | สร้าง Model พร้อม Migration |
| `php artisan route:list` | แสดงรายการ Route ทั้งหมด |

---

