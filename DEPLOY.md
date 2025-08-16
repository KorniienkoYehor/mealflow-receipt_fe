# 🚀 Інструкції по деплою на Railway

## 📋 Передумови

1. **GitHub репозиторій** - код повинен бути в GitHub
2. **Railway акаунт** - зареєструйтесь на [railway.app](https://railway.app)
3. **Node.js 18+** - для локальної збірки

## 🔧 Налаштування Railway

### 1. Підключення GitHub репозиторію

1. Увійдіть в Railway Dashboard
2. Натисніть "New Project"
3. Виберіть "Deploy from GitHub repo"
4. Виберіть ваш репозиторій `mealflow-receipt_fe`
5. Railway автоматично виявить Dockerfile

### 2. Конфігурація змінних середовища

В Railway Dashboard додайте наступні змінні:

```bash
NODE_ENV=production
PORT=3000
REACT_APP_MEALFLOW_BASE_URL=https://web-production-51d5.up.railway.app
REACT_APP_MEALFLOW_API_KEY=mealflow-api-key-2025-secure
```

### 3. Налаштування домену

1. В Railway Dashboard перейдіть в "Settings" → "Domains"
2. Railway автоматично надасть `.railway.app` домен
3. Можна додати власний домен (опціонально)

## 🐳 Docker конфігурація

### Dockerfile
Проект використовує багатоетапну збірку:
1. **Build stage** - встановлення залежностей та збірка React додатку
2. **Production stage** - встановлення `serve` та запуск статичного сервера

### Оптимізація образу
- Використовується Alpine Linux для меншого розміру
- Мультиетапна збірка для оптимізації
- Тільки production залежності в фінальному образі

## 📊 Моніторинг та логування

### Health Check
- **Path**: `/`
- **Timeout**: 300 секунд
- **Interval**: автоматично

### Логи
- Railway автоматично збирає логи
- Доступні в реальному часі в Dashboard
- Можна експортувати для аналізу

## 🔄 Автоматичний деплой

### GitHub Actions (опціонально)
Railway автоматично розгортає додаток при кожному push в `main` гілку.

### Ручний деплой
```bash
# Встановіть Railway CLI
npm install -g @railway/cli

# Увійдіть в Railway
railway login

# Розгорніть проект
railway up

# Перегляньте логи
railway logs

# Відкрийте додаток
railway open
```

## 🚨 Розв'язання проблем

### Помилка збірки
1. Перевірте логи в Railway Dashboard
2. Переконайтеся, що всі залежності в `package.json`
3. Перевірте Dockerfile на синтаксичні помилки

### Помилка запуску
1. Перевірте змінні середовища
2. Переконайтеся, що порт 3000 відкритий
3. Перевірте health check

### Проблеми з API
1. Перевірте Mealflow API ключ
2. Переконайтеся, що API доступне
3. Перевірте CORS налаштування

## 📈 Масштабування

### Автоматичне масштабування
Railway автоматично масштабує додаток залежно від навантаження.

### Ручне масштабування
В Railway Dashboard можна встановити:
- Кількість реплік
- Обмеження ресурсів
- Політику перезапуску

## 🔒 Безпека

### Змінні середовища
- Ніколи не комітьте `.env` файли
- Використовуйте Railway Secrets для чутливих даних
- Регулярно оновлюйте API ключі

### HTTPS
Railway автоматично надає SSL сертифікати для всіх доменів.

## 📞 Підтримка

- **Railway Docs**: [docs.railway.app](https://docs.railway.app)
- **GitHub Issues**: Створюйте issues в репозиторії
- **Discord**: Railway має активну спільноту

---

**Успішного деплою! 🎉**
