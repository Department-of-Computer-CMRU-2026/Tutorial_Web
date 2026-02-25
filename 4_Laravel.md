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

#### ขั้นตอนที่ 3: ตั้งค่าโปรเจกต์ (ครั้งแรก)

หลังสร้างโปรเจกต์ใหม่ Laravel จะมีไฟล์ `.env` อยู่แล้ว และจะรัน `php artisan key:generate` ให้อัตโนมัติ — ไม่ต้องทำซ้ำ

ถ้าเปิดโปรเจกต์เก่าที่ยังไม่มี key หรือย้ายเครื่อง ให้รัน:

```bash
cp .env.example .env
php artisan key:generate
```

- `.env` เก็บค่าสภาพแวดล้อม (รหัส DB, APP_KEY ฯลฯ) — **อย่า commit ไฟล์นี้ขึ้น Git**
- `key:generate` สร้างค่า `APP_KEY` สำหรับเข้ารหัส session/cookie

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
php artisan serve
```

**แบบรัน Frontend ด้วย (Vite + Laravel) — ตาม [Laravel 12.x](https://laravel.com/docs/12.x#creating-a-laravel-application):**

```bash
npm install && npm run build
composer run dev
```

- `composer run dev` จะรันทั้ง PHP server และ Vite (ถ้าโปรเจกต์มี frontend)
- เปิดเบราว์เซอร์ที่ **http://127.0.0.1:8000** หรือ **http://localhost:8000** จะเห็นหน้า welcome ของ Laravel

---

### ตัวเลือกเพิ่มเติมเมื่อสร้างโปรเจกต์

| วัตถุประสงค์ | คำสั่ง |
|--------------|--------|
| สร้างโปรเจกต์ในโฟลเดอร์ปัจจุบัน | `composer create-project laravel/laravel .` (ต้องเป็นโฟลเดอร์ว่าง) |
| กำหนดเวอร์ชัน Laravel | `composer create-project laravel/laravel my-app "12.*"` หรือ `"11.*"` |
| ติดตั้งแบบไม่รัน script (เช่น ไม่ถามยืนยัน) | `composer create-project laravel/laravel my-app --no-interaction` |

---

### รันเซิร์ฟเวอร์พัฒนา

```bash
php artisan serve
```

จากนั้นเปิดเบราว์เซอร์ที่: **http://127.0.0.1:8000** หรือ **http://localhost:8000**

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

 flow การทำงานแบบย่อ:

1. ผู้ใช้เปิด **URL** (เช่น `/about`) ในเบราว์เซอร์
2. Laravel ดูใน **routes** ว่า URL นี้ไปที่ไหน (เช่น ไปที่ Controller ตัวไหน, method ไหน)
3. **Controller** ทำงาน (อาจดึงข้อมูลจาก Model, คำนวณ ฯลฯ)
4. Controller **return View** หรือ **return redirect** หรือ **return response**
5. Laravel ส่ง **Response** กลับไปให้เบราว์เซอร์

ดังนั้น สิ่งที่เราต้องทำคือ: **กำหนด Route → เขียน Controller → สร้าง View (ถ้าเป็นหน้า HTML)**

---

## Routes — เส้นทาง URL

Route คือการบอก Laravel ว่า “เมื่อมีคนเรียก URL นี้ ให้ทำอะไร”

ไฟล์หลักสำหรับเว็บ: **`routes/web.php`**

### ตัวอย่างง่าย: แสดงข้อความอย่างเดียว

```php
use Illuminate\Support\Facades\Route;

Route::get('/', function () {
    return 'สวัสดี Laravel';
});

Route::get('/about', function () {
    return 'นี่คือหน้า About';
});
```

- `Route::get('/about', ...)` = ถ้าเปิด **GET** ไปที่ `/about` จะทำงานใน function
- `return '...'` = ส่งข้อความกลับไปแสดงบนหน้าเว็บ

### ใช้ Controller แทนการเขียน logic ใน Route

```php
use App\Http\Controllers\PageController;

Route::get('/', [PageController::class, 'home']);
Route::get('/about', [PageController::class, 'about']);
```

ความหมาย:

- เมื่อมีคนเปิด **GET /** → เรียก `PageController::home()`
- เมื่อมีคนเปิด **GET /about** → เรียก `PageController::about()`

### ประเภท Route ที่ใช้บ่อย

- `Route::get($uri, $action)` — เปิดหน้ามาตามลิงก์ (GET)
- `Route::post($uri, $action)` — ส่งฟอร์ม (POST)
- `Route::put($uri, $action)` — อัปเดต (PUT)
- `Route::delete($uri, $action)` — ลบ (DELETE)

ตัวอย่างรับฟอร์ม:

```php
Route::post('/contact', [ContactController::class, 'submit']);
```

---

## Controllers — จัดการ logic

Controller คือคลาสที่รับคำขอจาก Route แล้วจัดการ logic (ดึงข้อมูล, คำนวณ, เลือก View) แล้ว return ผลลัพธ์

### สร้าง Controller ด้วย Artisan

```bash
php artisan make:controller PageController
```

จะได้ไฟล์ที่ `app/Http/Controllers/PageController.php`

### ตัวอย่าง Controller

```php
<?php

namespace App\Http\Controllers;

class PageController extends Controller
{
    public function home()
    {
        return view('welcome');  // แสดง view ชื่อ welcome
    }

    public function about()
    {
        return view('about');   // แสดง view ชื่อ about
    }
}
```

- `view('welcome')` = ใช้ไฟล์ `resources/views/welcome.blade.php`
- `view('about')` = ใช้ไฟล์ `resources/views/about.blade.php`

### ส่งข้อมูลไปยัง View

```php
public function show($id)
{
    $user = User::find($id);
    return view('user.profile', ['user' => $user]);
    // หรือ
    return view('user.profile', compact('user'));
}
```

ใน View จะได้ตัวแปร `$user` ใช้ใน Blade ได้

---

## Views — หน้าเว็บที่ผู้ใช้เห็น

View ใน Laravel ใช้ engine ชื่อ **Blade** ไฟล์ลงท้าย `.blade.php` อยู่ที่ `resources/views/`

### ตัวอย่าง Blade พื้นฐาน

ไฟล์ `resources/views/welcome.blade.php`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>หน้าแรก</title>
</head>
<body>
    <h1>สวัสดี, {{ $name ?? 'ผู้มาเยือน' }}</h1>
</body>
</html>
```

- `{{ $name }}` = แสดงค่าของ `$name` (หลีกเลี่ยง XSS อัตโนมัติ)
- `{{ $name ?? 'ผู้มาเยือน' }}` = ถ้าไม่มี `$name` ให้แสดง 'ผู้มาเยือน'

### ส่งตัวแปรจาก Controller

```php
return view('welcome', ['name' => 'สมชาย']);
```

### Blade ที่ใช้บ่อย

- แสดงค่า: `{{ $variable }}`
- PHP บรรทัดเดียว: `@if`, `@else`, `@endif`, `@foreach`, `@endforeach`
- ใช้ layout: `@extends('layouts.app')`, `@section('content')` ... `@endsection`

ตัวอย่าง layout แบบสั้น:

**layouts/app.blade.php**

```html
<!DOCTYPE html>
<html>
<head><title>@yield('title')</title></head>
<body>
    @yield('content')
</body>
</html>
```

**pages/about.blade.php**

```html
@extends('layouts.app')

@section('title', 'เกี่ยวกับเรา')

@section('content')
    <h1>เกี่ยวกับเรา</h1>
    <p>เนื้อหาหน้า about</p>
@endsection
```

---

## Models และฐานข้อมูล

**Model** ใน Laravel คือตัวแทน **ตารางในฐานข้อมูล** ใช้ผ่าน **Eloquent ORM**

- หนึ่ง Model มักเทียบกับหนึ่งตาราง (เช่น `User` → ตาราง `users`)
- ใช้ Model เพื่อ **อ่าน / สร้าง / แก้ไข / ลบ** แถวในตาราง โดยไม่ต้องเขียน SQL เองมาก

### สร้าง Model

```bash
php artisan make:model Product
```

จะได้ไฟล์ `app/Models/Product.php` (Laravel 8+ อยู่ที่ `app/Models/`)

### ตัวอย่าง Model

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Product extends Model
{
    protected $table = 'products';  // ชื่อตาราง (ถ้าไม่ใส่ จะใช้พหูพจน์ของชื่อคลาส)
    protected $fillable = ['name', 'price', 'description'];  // ฟิลด์ที่อนุญาตให้ assign เป็น mass
}
```

- `$fillable` = ฟิลด์ที่อนุญาตให้ใช้ `Product::create([...])` หรือ `$product->update([...])` ได้อย่างปลอดภัย

---

## Migration — สร้าง/แก้ไขตาราง

**Migration** คือไฟล์ที่บรรยายว่า “จะสร้างหรือแก้ไขตารางอย่างไร” ทำให้โครงสร้างฐานข้อมูลเป็น version ได้ และทำซ้ำบนเครื่องอื่นได้

### สร้าง Migration

```bash
php artisan make:migration create_products_table
```

จะได้ไฟล์ใน `database/migrations/` ชื่อประมาณ `xxxx_xx_xx_xxxxxx_create_products_table.php`

### ตัวอย่าง Migration สร้างตาราง

```php
public function up()
{
    Schema::create('products', function (Blueprint $table) {
        $table->id();
        $table->string('name');
        $table->decimal('price', 8, 2);
        $table->text('description')->nullable();
        $table->timestamps();  // created_at, updated_at
    });
}

public function down()
{
    Schema::dropIfExists('products');
}
```

- `up()` = เมื่อรัน migration (สร้างตาราง)
- `down()` = เมื่อ rollback (ลบตาราง)

### รัน Migration

ก่อนรัน ต้องตั้งค่า DB ในไฟล์ **`.env`** ให้ถูกต้อง:

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=root
DB_PASSWORD=
```

จากนั้นรัน:

```bash
php artisan migrate
```

---

## Eloquent ORM — ดึงและบันทึกข้อมูล

### ดึงข้อมูล (Read)

```php
// ทุกแถว
$products = Product::all();

// ค้นหาจาก id
$product = Product::find(1);

// เงื่อนไข
$products = Product::where('price', '>', 100)->get();

// แรกแถวเดียว
$product = Product::where('name', 'เสื้อ')->first();
```

### สร้างข้อมูล (Create)

```php
Product::create([
    'name'        => 'เสื้อคอกลม',
    'price'       => 299,
    'description' => 'ผ้าฝ้าย',
]);
```

ฟิลด์ที่ใส่ต้องอยู่ใน `$fillable` ของ Model

### แก้ไข (Update)

```php
$product = Product::find(1);
$product->name = 'เสื้อแขนยาว';
$product->save();

// หรือ
$product->update(['name' => 'เสื้อแขนยาว']);
```

### ลบ (Delete)

```php
$product = Product::find(1);
$product->delete();
```

---

## Form และ Validation

### รับค่าจากฟอร์มใน Controller

```php
use Illuminate\Http\Request;

public function store(Request $request)
{
    $name = $request->input('name');
    $email = $request->input('email');
    // หรือ
    $name = $request->name;
}
```

### Validation แบบพื้นฐาน

```php
$validated = $request->validate([
    'name'  => 'required|string|max:255',
    'email' => 'required|email',
    'age'   => 'nullable|integer|min:1|max:120',
]);
// ถ้าไม่ผ่านจะ redirect กลับพร้อม error อัตโนมัติ
// ถ้าผ่าน $validated จะมีเฉพาะฟิลด์ที่กำหนดและผ่านกฎแล้ว
```

กฎที่ใช้บ่อย: `required`, `string`, `email`, `integer`, `min:`, `max:`, `nullable`, `unique:table,column`

### แสดง Error ใน View (Blade)

```html
@if ($errors->any())
    <ul>
        @foreach ($errors->all() as $error)
            <li>{{ $error }}</li>
        @endforeach
    </ul>
@endif
```

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
| `php artisan tinker` | เปิด PHP REPL ในโปรเจกต์ (ลอง Model ได้) |

---

## สรุปแนวทางสำหรับมือใหม่

1. **เริ่มจาก Route** — เปิด `routes/web.php` กำหนด URL กับ Controller/method
2. **สร้าง Controller** — `php artisan make:controller ...` แล้วเขียน method รับ request, คืน view หรือ redirect
3. **สร้าง View** — ใส่ไฟล์ `.blade.php` ใน `resources/views/` แล้วใช้ `return view('ชื่อ');` ใน Controller
4. **ใช้ Model เมื่อมีฐานข้อมูล** — สร้าง Model + Migration แล้วใช้ Eloquent ใน Controller เพื่อดึง/บันทึกข้อมูล
5. **รับฟอร์มด้วย Request** — ใช้ `$request->validate([...])` เพื่อตรวจข้อมูล แล้วค่อยบันทึกลง Model
6. **ฝึกใช้ `php artisan route:list`** — ช่วยให้เห็นภาพว่า URL ไปที่ไหน
7. **อ่าน Error ในหน้าเว็บและในเทอร์มินัล** — Laravel แจ้งข้อผิดพลาดค่อนข้างชัด

ถ้าทำตามขั้นตอนนี้และลองเขียนหน้าเล็กๆ หนึ่งหน้า (เช่น หน้ารายการสินค้า + ฟอร์มเพิ่มสินค้า) จะเริ่มคุ้นกับ flow ของ Laravel ได้เร็ว

---

*คู่มือนี้เขียนสำหรับมือใหม่ อ่านแล้วเข้าใจง่าย และสามารถนำไปปฏิบัติตามได้ทันที*
