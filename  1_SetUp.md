# Setup — การติดตั้ง

เอกสารนี้สอนเฉพาะ **การติดตั้ง** เท่าที่สอนได้ ไม่รวมการใช้งานหรือแนวทางปฏิบัติ

---

## สารบัญ

1. [Git](#git)
2. [Docker Desktop](#docker-desktop)
3. [Node.js](#nodejs)
4. [Bun](#bun)
5. [Composer](#composer)
6. [Laravel](#laravel)
7. [DBeaver](#dbeaver)
8. [FileZilla](#filezilla)
9. [Google Antigravity](#google-antigravity)

---

## Git

- **Windows:** ดาวน์โหลดจาก [git-scm.com](https://git-scm.com) แล้วติดตั้ง
- **macOS:** เปิด Terminal แล้วรัน `xcode-select --install` หรือ `brew install git`
- **Linux (Ubuntu/Debian):** `sudo apt update && sudo apt install git`

ตรวจสอบ:

```bash
git --version
```

---

## Docker Desktop

- ดาวน์โหลดจาก [docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop) แล้วติดตั้ง
- เปิด Docker Desktop ให้รันอยู่ก่อนใช้คำสั่ง `docker`

ตรวจสอบ:

```bash
docker --version
docker compose version
```

---

## Node.js

- ดาวน์โหลด LTS จาก [nodejs.org](https://nodejs.org) แล้วติดตั้ง (ได้ทั้ง `node` และ `npm`)
- **macOS (Homebrew):** `brew install node`
- **Linux (Ubuntu/Debian):** `sudo apt update && sudo apt install nodejs npm`

ตรวจสอบ:

```bash
node --version
npm --version
```

---

## Bun

- **macOS / Linux:** `curl -fsSL https://bun.sh/install | bash` (จากนั้นเปิด shell ใหม่หรือรัน `source ~/.bashrc` / `source ~/.zshrc`)
- **Windows:** ใช้ WSL แล้วรันคำสั่งด้านบน หรือติดตั้งผ่าน npm: `npm install -g bun`

ตรวจสอบ:

```bash
bun --version
```

---

## Composer

- ติดตั้งหลังมี PHP แล้ว: [getcomposer.org/download](https://getcomposer.org/download/)
- **Windows:** ใช้ installer จากลิงก์ด้านบน
- **macOS / Linux:** รันคำสั่งจากหน้า Download (ตัวอย่าง):

```bash
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php composer-setup.php
php -r "unlink('composer-setup.php');"
sudo mv composer.phar /usr/local/bin/composer
```

ตรวจสอบ:

```bash
composer --version
```

---

## Laravel

- ติดตั้งหลังมี Composer แล้ว:

```bash
composer global require laravel/installer
```

ให้แน่ใจว่า path ของ `~/.composer/vendor/bin` อยู่ใน PATH (เพิ่มใน `~/.bashrc` หรือ `~/.zshrc`)

ตรวจสอบ:

```bash
laravel --version
```

---

## DBeaver

- ดาวน์โหลดจาก [dbeaver.io](https://dbeaver.io/download/) เลือก Community Edition แล้วติดตั้งตามตัวติดตั้งของแต่ละ OS

---

## FileZilla

- ดาวน์โหลดจาก [filezilla-project.org](https://filezilla-project.org/download.php?type=client) แล้วติดตั้ง

---

## Google Antigravity

- ดาวน์โหลดจาก [antigravity.google/download](https://antigravity.google/download) เลือกตาม OS:
  - **macOS:** Apple Silicon หรือ Intel (ต้อง macOS 12 Monterey ขึ้นไป)
  - **Windows:** x64 หรือ ARM64 (ต้อง Windows 10 64-bit ขึ้นไป)
  - **Linux:** ต้อง glibc ≥ 2.28 (เช่น Ubuntu 20, Debian 10, Fedora 36, RHEL 8)
- เปิดตัวติดตั้งแล้วทำตามขั้นตอนบนหน้าจอ
- ต้องมี Chrome และบัญชี Gmail (ช่วง preview รองรับบัญชีส่วนตัว)

