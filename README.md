# Symfony 6 + PostgreSQL на Ubuntu 22.04

## Описание

Учебный проект Symfony 6 с базой PostgreSQL, установленный и настроенный вручную на Ubuntu 22.04.

---

## Установка и настройка

### 1. Установка PHP и необходимых расширений


```bash
sudo apt update
sudo apt install php php-cli php-common php-curl php-intl php-mbstring php-xml php-zip php-pgsql php-bcmath php-sqlite3 unzip curl git -y
```

### 2. Установка и настройка PostgreSQL

#### Установите PostgreSQL и необходимые компоненты:
```bash
sudo apt install postgresql postgresql-contrib -y
```

#### Запустите и включите сервис PostgreSQL:
```bash
sudo systemctl start postgresql
sudo systemctl enable postgresql
```

#### Создайте пользователя (роль) и базу данных для проекта:
```bash
sudo -u postgres psql
```
#### Внутри консоли PostgreSQL выполните:
```sql
CREATE ROLE symfony WITH LOGIN PASSWORD 'your_password_here';
CREATE DATABASE symfony_db OWNER symfony;
GRANT ALL PRIVILEGES ON DATABASE symfony_db TO symfony;
\q
```
#### Настройте подключение в .env вашего Symfony проекта:
```env
DATABASE_URL="pgsql://symfony:your_password_here@127.0.0.1:5432/symfony_db"
```

#### Очистка кеша Symfony (при необходимости)
```bash
php bin/console cache:clear
```

### Использование

##### Запустить локальный сервер Symfony:
```bash
symfony server:start
```

##### Войти в базу данных PostgreSQL:
```bash
psql -U symfony -d symfony_db
```



