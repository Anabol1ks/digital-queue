# Digital Queue

> **Система управления онлайн-очередью для практических занятий**

![Go](https://img.shields.io/badge/backend-go-00ADD8?logo=go) ![React](https://img.shields.io/badge/frontend-react-61DAFB?logo=react) ![Docker](https://img.shields.io/badge/docker-2496ED?logo=docker) ![PostgreSQL](https://img.shields.io/badge/database-postgresql-4169E1?logo=postgresql) ![Redis](https://img.shields.io/badge/cache-redis-DC382D?logo=redis)

## О проекте

Digital Queue — это высокопроизводительное решение для онлайн-управления очередями студентов на практических занятиях и лабораторных работах. Проект состоит из двух основных компонентов:

- **Backend** на Go: реализует REST API и WebSocket‑соединения для realtime-обновлений, а также фоновые задачи по автоматическому открытию/закрытию очередей по расписанию. Подробнее в [backend README](https://github.com/Anabol1ks/digital-queue-backend).
- **Frontend** на React + Vite: одностраничное приложение для интерактивного отображения групп, расписания и очередей. Подробнее в [frontend README](https://github.com/imurbestfriend/digital-queue-frontend).

Систему можно запускать как локально для разработки, так и в контейнерах Docker без изменения кода.

## Основные возможности

- Регистрация и аутентификация пользователей через JWT
- Управление группами и расписанием занятий (PostgreSQL + Redis)
- Создание, присоединение и выход из очередей
- Realtime-обновления очередей по WebSocket
- Автоматическое открытие/закрытие очередей по расписанию
- Полная контейнеризация с помощью Docker Compose

## Структура репозитория

```bash
digital-queue/
├── backend/           # Go-сервис (подмодуль)
├── frontend/          # React-приложение (подмодуль)
└── docker-compose.yml # Конфигурация для Docker Compose
``` 

## Требования

- Go 1.23+
- Node.js 20+
- Docker & Docker Compose

## Быстрый старт

### 1. Клонировать репозиторий с подмодулями

```bash
git clone --recurse-submodules https://github.com/Anabol1ks/digital-queue.git
cd digital-queue
```

### 2. Запуск локальной разработки

#### Backend

```bash
cd backend
cp .env.example .env            # скопируйте .env.example → .env и заполните параметры БД, Redis, JWT
go mod download                 # установить зависимости
go run main.go                  # запустить сервер на http://localhost:8080
```

*Swagger UI:* http://localhost:8080/swagger/index.html

#### Frontend

```bash
cd frontend
cp .env.example .env            # скопируйте .env.example → .env
npm ci                          # установить зависимости
# отредактируйте .env:
# VITE_API_URL=http://localhost:8080
# VITE_WS_URL=ws://localhost:8080
npm run dev                     # запустить приложение на http://localhost:5173
```

### 3. Запуск через Docker

Перед запуском убедитесь, что:

- В файлах `backend/.env` и `frontend/.env` указаны актуальные значения переменных.
- В `docker-compose.yml` разделы `environment` для сервисов `db` и `db_test` (POSTGRES_PASSWORD, POSTGRES_DB и т. д.) соответствуют вашим `DB_PASSWORD`, `TEST_DB_PASSWORD`, `DB_NAME` и прочим в `backend/.env`.

```bash
docker-compose up --build
```

- **Backend:** http://localhost:8080
- **Frontend:** http://localhost:5173

## Дополнительные материалы

- Полная документация и примеры использования API содержатся в [backend README](https://github.com/Anabol1ks/digital-queue-backend).
- Гайды по настройке и расширению фронтенда доступны в [frontend README](https://github.com/imurbestfriend/digital-queue-frontend).

## Вклад

PR и идеи приветствуются! Пожалуйста, открывайте issues для обсуждения новых фич или багов.

---

© 2025 Digital Queue. Все права защищены.
