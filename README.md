# Football Academy Management System

Система управління футбольною академією для тренерів, гравців та батьків.

## Опис

Веб-застосунок для управління футбольною академією, який дозволяє:
- Адміністраторам керувати користувачами, групами та подіями
- Тренерам планувати тренування та матчі, відмічати відвідуваність, оцінювати гравців
- Гравцям переглядати розклад та свою статистику
- Батькам слідкувати за успіхами своїх дітей

## Функціонал

### Користувачі та ролі
- **Admin** - повний доступ до всіх функцій
- **Coach** - управління тренуваннями та матчами своїх груп
- **Player** - перегляд розкладу та особистої статистики
- **Parent** - перегляд статистики дітей

### Управління групами
- Створення вікових груп (U-7, U-9, U-11, тощо)
- Призначення головного тренера та асистентів
- Додавання/видалення гравців

### Тренування
- Планування тренувань з темою та локацією
- Автоматична генерація тренувань за тижневим графіком
- Відмітка відвідуваності (Present, Late, Absent, Excused)
- Оцінювання гравців за різними критеріями (1-10)

### Матчі
- Планування матчів з суперником та локацією
- Фіксація результатів (голи, асисти для кожного гравця)
- Відмітка відвідуваності

### Календар
- Візуальний календар всіх подій
- Фільтрація за групами
- Швидкий перегляд деталей

### Статистика
- Статистика гравця: матчі, голи, асисти, відвідуваність
- Командна статистика для тренерів
- Батьківський доступ до статистики дітей

## Технології

### Backend
- **NestJS** - Node.js фреймворк
- **TypeORM** - ORM для роботи з базою даних
- **PostgreSQL** - реляційна база даних
- **JWT** - аутентифікація
- **bcrypt** - хешування паролів

### Frontend
- **React 19** - UI бібліотека
- **TypeScript** - типізація
- **Vite** - збірка та dev-сервер
- **Tailwind CSS 4** - стилізація
- **React Router 7** - маршрутизація
- **Axios** - HTTP клієнт

### Інфраструктура
- **Docker Compose** - контейнеризація сервісів
- **PostgreSQL 15** - база даних (порт 5433)
- **pgAdmin 4** - веб-інтерфейс для БД (порт 5050)
- **Redis** - кешування (порт 6379)

## Структура проекту

```
F-academy/
├── backend/                 # NestJS API
│   ├── src/
│   │   ├── auth/           # Аутентифікація (JWT, guards)
│   │   ├── users/          # Користувачі
│   │   ├── coaches/        # Тренери
│   │   ├── players/        # Гравці
│   │   ├── parents/        # Батьки
│   │   ├── groups/         # Групи
│   │   ├── events/         # Тренування, матчі, графіки
│   │   ├── attendance/     # Відвідуваність
│   │   ├── evaluations/    # Оцінки
│   │   ├── common/         # Спільні сутності
│   │   └── database/       # Seeds
│   └── package.json
├── frontend/               # React SPA
│   ├── src/
│   │   ├── api/           # API клієнти
│   │   ├── components/    # Компоненти (ProtectedRoute, тощо)
│   │   ├── contexts/      # React контексти (Auth)
│   │   ├── pages/         # Сторінки
│   │   └── types/         # TypeScript типи
│   └── package.json
├── docker-compose.yml      # Docker сервіси
└── README.md
```

## Встановлення

### Вимоги
- Node.js 18+
- Docker та Docker Compose
- npm або yarn

### 1. Клонування репозиторію
```bash
git clone <repo-url>
cd F-academy
```

### 2. Запуск Docker сервісів
```bash
docker-compose up -d
```

Це запустить:
- PostgreSQL на порті `5433`
- pgAdmin на порті `5050`
- Redis на порті `6379`

### 3. Налаштування Backend
```bash
cd backend
npm install
```

Створіть файл `.env`:
```env
DATABASE_HOST=localhost
DATABASE_PORT=5433
DATABASE_USER=postgres
DATABASE_PASSWORD=postgres
DATABASE_NAME=football_academy

JWT_SECRET=your-super-secret-jwt-key
JWT_EXPIRES_IN=7d
```

### 4. Налаштування Frontend
```bash
cd frontend
npm install
```

## Запуск

### Backend (порт 3000)
```bash
cd backend
npm run start:dev
```

### Frontend (порт 5173)
```bash
cd frontend
npm run dev
```

## Початкові дані

### Створення адміністратора
```bash
cd backend
npm run seed:admin
```
Створює користувача:
- Email: `admin@footballacademy.com`
- Password: `admin123`

### Тестові дані
```bash
cd backend
npm run seed:test-data
```
Створює:
- 3 тренерів
- 2 групи (U-19, U-17)
- 10 гравців
- 2 батьків (з прив'язкою до дітей)
- 5 тренувань
- 2 матчі з результатами

**Тестові акаунти:**
| Роль | Email | Пароль |
|------|-------|--------|
| Admin | admin@footballacademy.com | admin123 |
| Coach | coach1@footballacademy.com | coach123 |
| Coach | coach2@footballacademy.com | coach123 |
| Player | player1@footballacademy.com | player123 |
| Parent | parent1@footballacademy.com | parent123 |

## API Endpoints

### Auth
- `POST /auth/login` - вхід в систему

### Users
- `GET /users` - список користувачів (Admin)
- `POST /users` - створення користувача (Admin)
- `PATCH /users/:id` - оновлення (Admin)
- `DELETE /users/:id` - видалення (Admin)

### Groups
- `GET /groups` - всі групи (Admin)
- `GET /groups/my` - мої групи (Coach, Player, Parent)
- `POST /groups` - створення (Admin)
- `PATCH /groups/:id` - оновлення (Admin)
- `PATCH /groups/:id/staff` - призначення тренерів (Admin)
- `POST /groups/:id/players` - додати гравців (Admin)
- `DELETE /groups/:id/players` - видалити гравців (Admin)

### Trainings
- `GET /trainings` - список тренувань
- `POST /trainings` - створення (Admin, Coach)
- `GET /trainings/:id` - деталі
- `PATCH /trainings/:id` - оновлення (Admin, Coach)
- `DELETE /trainings/:id` - видалення (Admin, Coach)

### Matches
- `GET /matches` - список матчів
- `POST /matches` - створення (Admin, Coach)
- `GET /matches/:id` - деталі з результатами
- `PATCH /matches/:id` - оновлення (Admin, Coach)
- `PUT /matches/:id/goals` - оновити голи (Admin, Coach)
- `DELETE /matches/:id` - видалення (Admin, Coach)

### Attendance
- `GET /attendance/training/:id` - відвідуваність тренування
- `PUT /attendance/training/:id` - оновити відвідуваність
- `GET /attendance/match/:id` - відвідуваність матчу
- `PUT /attendance/match/:id` - оновити відвідуваність
- `GET /attendance/my/stats` - моя статистика (Player)

### Evaluations
- `GET /evaluations/training/:id` - оцінки тренування
- `PUT /evaluations/training/:id` - оновити оцінки (Coach)

### Schedules
- `GET /groups/:id/schedule` - графік групи
- `PUT /groups/:id/schedule` - оновити графік
- `POST /groups/:id/schedule/generate` - згенерувати тренування
- `DELETE /groups/:id/schedule/trainings` - видалити згенеровані

### Players
- `GET /players/stats/my` - моя статистика (Player)
- `GET /players/stats/team/:groupId` - статистика команди (Coach)
- `GET /players/stats/children` - статистика дітей (Parent)

### Calendar
- `GET /calendar` - події календаря

## pgAdmin

Доступ: http://localhost:5050
- Email: `admin@footballacademy.com`
- Password: `admin`

Підключення до БД:
- Host: `postgres` (в Docker мережі) або `localhost`
- Port: `5432` (в Docker) або `5433` (зовні)
- Database: `football_academy`
- User: `postgres`
- Password: `postgres`

## Ліцензія

MIT
