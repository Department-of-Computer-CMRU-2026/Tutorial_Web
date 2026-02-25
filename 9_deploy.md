## 1. ติดตั้ง Laravel

### 1.1 Clone โปรเจกต์และตั้งค่า `.env`

```bash
# Clone repository
git clone <your-repo-url>
cd <project-folder>

# คัดลอกไฟล์ environment
cp .env.example .env
```

### 1.2 ติดตั้ง Dependencies และเริ่ม Container

```bash
# ติดตั้ง Composer dependencies
docker compose run --rm app composer install

# เริ่ม containers ทั้งหมด
docker compose up -d
```

### 1.3 ตั้งค่า Permissions

```bash
# กำหนดสิทธิ์ storage และ cache
docker compose exec -u 0 app chown -R www-data:www-data storage bootstrap/cache
docker compose exec -u 0 app chmod -R 777 storage bootstrap/cache

# กำหนดสิทธิ์ .env
docker compose exec -u 0 app chown www-data:www-data .env
docker compose exec -u 0 app chmod 664 .env
```

### 1.4 ตั้งค่า Laravel

```bash
# สร้าง Application Key
docker compose exec app php artisan key:generate

# รัน Database Migration
docker compose exec app php artisan migrate

# สร้าง Storage Link
docker compose exec -u 0 app php artisan storage:link
```

> ⚠️ **หมายเหตุ:** หากต้องการแก้ไข `.env` หลังจากนี้:
> ```bash
> rm .env
> # แก้ไขค่าใน .env.example แล้วรัน cp อีกครั้ง
> cp .env.example .env
> docker compose exec app php artisan key:generate
> ```

---

##2 ตัวอย่าง `.env` สำหรับนักศึกษา

```env
COMPOSE_PROJECT_NAME=std65123800   # ← เปลี่ยนเป็น Student ID ของตัวเอง
WEB_PORT=8080                       # ← เปลี่ยน port ให้ไม่ซ้ำกัน

DB_CONNECTION=pgsql
DB_HOST=db
DB_PORT=5432
DB_DATABASE=laravel
DB_USERNAME=laravel
DB_PASSWORD=secret
```

---
