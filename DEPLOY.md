# Деплой на бесплатный хостинг

## 1. Frontend (Vercel)

### Автоматический деплой:

1. Перейдите на https://vercel.com
2. Войдите через GitHub аккаунт `tolmaswork`
3. Нажмите "Add New Project"
4. Выберите репозиторий `antiplagiat-by`
5. Настройки:
   - **Framework Preset**: Create React App
   - **Root Directory**: `frontend`
   - **Build Command**: `npm run build`
   - **Output Directory**: `build`
   - **Install Command**: `npm install`

6. Environment Variables (добавьте):
   ```
   REACT_APP_API_URL=https://your-backend-url.railway.app/api
   REACT_APP_NAME=Antiplagiat.by
   ```

7. Нажмите "Deploy"

### Или через CLI:

```bash
cd frontend
npm install -g vercel
vercel login
vercel --prod
```

---

## 2. Backend (Railway)

### Автоматический деплой:

1. Перейдите на https://railway.app
2. Войдите через GitHub аккаунт `tolmaswork`
3. Нажмите "New Project"
4. Выберите "Deploy from GitHub repo"
5. Выберите `antiplagiat-by`
6. Railway автоматически определит Node.js проект

### Настройка:

1. В настройках проекта укажите:
   - **Root Directory**: `backend`
   - **Build Command**: `npm install && npm run build`
   - **Start Command**: `npm start`

2. Добавьте PostgreSQL:
   - В проекте нажмите "New" → "Database" → "Add PostgreSQL"
   - Railway автоматически создаст `DATABASE_URL`

3. Добавьте переменные окружения (Settings → Variables):
   ```
   PORT=5000
   NODE_ENV=production
   DATABASE_URL=${{Postgres.DATABASE_URL}}
   JWT_SECRET=your-super-secret-jwt-key-change-this-in-production
   CORS_ORIGIN=https://your-frontend-url.vercel.app
   REDIS_URL=redis://default:password@redis-host:6379
   ```

4. Выполните миграции:
   - Подключитесь к PostgreSQL через Railway CLI или pgAdmin
   - Выполните SQL из `backend/migrations/001_initial_schema.sql`

### Или через CLI:

```bash
npm install -g @railway/cli
railway login
railway init
railway up
```

---

## 3. База данных (Supabase) - Альтернатива

Если хотите использовать Supabase вместо Railway PostgreSQL:

1. Перейдите на https://supabase.com
2. Создайте новый проект
3. В SQL Editor выполните миграции из `backend/migrations/001_initial_schema.sql`
4. Скопируйте Connection String из Settings → Database
5. Используйте его как `DATABASE_URL` в Railway

---

## 4. Redis (Upstash) - Опционально

1. Перейдите на https://upstash.com
2. Создайте Redis базу (бесплатный план)
3. Скопируйте Redis URL
4. Добавьте как `REDIS_URL` в Railway

---

## 5. Финальные шаги

1. После деплоя backend на Railway, скопируйте URL (например: `https://antiplagiat-by-production.up.railway.app`)

2. Обновите `REACT_APP_API_URL` в Vercel:
   ```
   REACT_APP_API_URL=https://antiplagiat-by-production.up.railway.app/api
   ```

3. Обновите `CORS_ORIGIN` в Railway:
   ```
   CORS_ORIGIN=https://your-app.vercel.app
   ```

4. Redeploy оба проекта

---

## Проверка

1. Откройте ваш Vercel URL (например: `https://antiplagiat-by.vercel.app`)
2. Зарегистрируйтесь
3. Загрузите тестовый файл
4. Проверьте результаты

---

## Мониторинг

- **Vercel**: https://vercel.com/dashboard
- **Railway**: https://railway.app/dashboard
- **Логи**: Доступны в дашбордах обоих сервисов

---

## Лимиты бесплатных планов

### Vercel:
- 100GB bandwidth/месяц
- Безлимитные деплои
- Автоматический SSL

### Railway:
- $5 кредитов/месяц (≈500 часов)
- 1GB RAM
- 1GB диска

### Supabase:
- 500MB база данных
- 2GB bandwidth
- 50,000 monthly active users

---

## Troubleshooting

### Backend не запускается:
- Проверьте логи в Railway
- Убедитесь, что все env переменные установлены
- Проверьте, что миграции выполнены

### Frontend не подключается к backend:
- Проверьте `REACT_APP_API_URL`
- Проверьте `CORS_ORIGIN` в backend
- Откройте DevTools → Network для проверки запросов

### База данных не подключается:
- Проверьте `DATABASE_URL`
- Убедитесь, что PostgreSQL запущен
- Проверьте, что миграции выполнены
