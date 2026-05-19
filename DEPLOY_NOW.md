# 🚀 Инструкция по деплою (открыты страницы в браузере)

## Я открыл для вас 2 страницы:

### 1. Vercel (Frontend) - уже открыта в браузере
**Что делать:**
1. Войдите через GitHub (tolmaswork)
2. Подтвердите доступ к репозиторию `antiplagiat-by`
3. Настройки:
   - Root Directory: `frontend` (нажмите Edit и выберите)
   - Framework: Create React App
   - Build Command: `npm run build`
   - Output Directory: `build`
4. Добавьте Environment Variables:
   - `REACT_APP_API_URL` = `https://ОСТАВЬТЕ_ПУСТЫМ` (обновим позже)
   - `REACT_APP_NAME` = `Antiplagiat.by`
5. Нажмите **Deploy**
6. **Скопируйте URL** после деплоя (например: `https://antiplagiat-by-xxx.vercel.app`)

---

### 2. Railway (Backend) - уже открыта в браузере
**Что делать:**
1. Войдите через GitHub (tolmaswork)
2. Выберите **"Deploy from GitHub repo"**
3. Найдите и выберите `antiplagiat-by`
4. После создания проекта:
   - Откройте Settings
   - Root Directory: `backend`
   - Build Command: `npm install && npm run build`
   - Start Command: `npm start`

5. **Добавьте PostgreSQL:**
   - Нажмите "New" → "Database" → "Add PostgreSQL"
   - Дождитесь создания

6. **Добавьте Variables** (Settings → Variables):
   ```
   PORT=5000
   NODE_ENV=production
   JWT_SECRET=antiplagiat_super_secret_key_2026
   CORS_ORIGIN=https://ваш-vercel-url.vercel.app
   ```
   (Замените на ваш URL из шага 1)

7. **Скопируйте Backend URL** (Settings → Domains)

---

## После деплоя обоих:

### 3. Выполните миграции БД
1. В Railway откройте PostgreSQL сервис
2. Перейдите в **Data** → **Query**
3. Скопируйте содержимое файла `backend/migrations/001_initial_schema.sql`
4. Вставьте и нажмите **Run Query**

### 4. Обновите Frontend
1. Вернитесь в Vercel
2. Settings → Environment Variables
3. Измените `REACT_APP_API_URL` на:
   ```
   https://ваш-railway-url.up.railway.app/api
   ```
4. Deployments → Redeploy

---

## ✅ Готово!

После этого ваш сайт будет работать!

**Напишите мне, когда:**
- Завершите деплой на Vercel (пришлите URL)
- Завершите деплой на Railway (пришлите URL)
- Если возникнут ошибки

Я помогу с миграциями и финальной настройкой!
