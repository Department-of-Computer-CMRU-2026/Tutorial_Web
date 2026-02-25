## 1. ติดตั้ง Laravel บน Server

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
# Student Configuration
# Change '66xxxxxx' to your Student ID (e.g. 66123456)
# Web Port: Any unique port (e.g. 8000 + last 2 digits)
STUDENT_ID=std66xxxxxx
STUDENT_NAME=std66xxxxxx
COMPOSE_PROJECT_NAME=std66xxxxxx
STUDENT_PORT=6xxx
FORWARD_DB_PORT=6xxx

# Database Configuration
# Hostname: std{ID}-db
# Database Port: Any unique port (e.g. 5400 + last 2 digits)
DB_CONNECTION=pgsql
DB_HOST=std66xxxxxx-db
DB_PORT=5432
DB_DATABASE=db_name
DB_USERNAME=db_66xxxxxx
DB_PASSWORD=db_password
```

---
