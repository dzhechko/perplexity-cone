# Клон Perplexity AI

Современный поисковый интерфейс с AI-функциональностью, похожий на Perplexity AI, построенный с использованием Next.js, React и TypeScript.

## Возможности

- 🔍 AI-поиск с использованием Exa.ai
- 🤖 Суммаризация результатов с помощью GPT-4
- 🎯 Несколько режимов поиска (Сфокусированный/Помощник/Написание)
- ⚡ Поиск в реальном времени с debouncing
- 📚 Разворачиваемые источники цитат
- 🎨 Современный UI с тёмной/светлой темой
- 📱 Полностью адаптивный дизайн

## Требования

- Node.js 16.x или выше
- npm или yarn
- OpenAI API ключ
- Exa.ai API ключ
- Serper.dev API ключ (опционально)

## Установка

1. Клонируйте репозиторий:

```bash
git clone [repository-url]
cd perplexity-clone
```

2. Установите зависимости:

```bash
npm install
```

3. Скопируйте файл с примером переменных окружения:

```bash
cp .env.example .env.local
```

4. Настройте переменные окружения в файле `.env.local`:

```env
# Режим отладки для подробного логирования
NEXT_PUBLIC_DEBUG=true

# Конфигурация OpenAI
OPENAI_API_KEY=ваш_openai_api_ключ
OPENAI_BASE_URL=https://api.openai.com/v1  # или ваш кастомный endpoint
OPENAI_MODEL=gpt-4  # или другие доступные модели
OPENAI_TEMPERATURE=0.3
OPENAI_MAX_TOKENS=1000

# API ключи поисковых провайдеров
NEXT_PUBLIC_EXA_API_KEY=ваш_exa_api_ключ
NEXT_PUBLIC_SERPER_API_KEY=ваш_serper_api_ключ  # опционально

# Окружение Node
NODE_ENV=development
```

Доступные модели OpenAI:
- Для стандартного OpenAI API: gpt-4, gpt-4-turbo-preview, gpt-3.5-turbo
- Для кастомных endpoints: уточняйте у вашего провайдера

5. Запустите сервер разработки:

```bash
npm run dev
```

6. Откройте [http://localhost:3000](http://localhost:3000) в браузере

## Режимы поиска

Приложение поддерживает три различных режима поиска:

### Сфокусированный режим (Focused)
- Краткие, основанные на фактах ответы
- Использует самые свежие источники (последние 24 часа)
- Возвращает меньше, но более релевантных результатов
- Лучше всего для: Быстрых фактов и актуальной информации

### Режим помощника (Copilot)
- Подробные объяснения с контекстом
- Сбалансированный выбор источников
- Включает примеры и связанную информацию
- Лучше всего для: Изучения и понимания тем

### Режим написания (Writing)
- Хорошо структурированные, комплексные ответы
- Использует более широкий временной диапазон для источников
- Включает больше контекста и бэкграунда
- Лучше всего для: Создания контента и исследований

## Структура проекта

- `/app` - Страницы и layouts Next.js app router
- `/components` - React компоненты
- `/lib` - Утилиты и интеграции с API
- `/types` - TypeScript определения типов
- `/hooks` - Пользовательские React хуки

## Разработка

- `npm run dev` - Запуск сервера разработки
- `npm run build` - Сборка для продакшена
- `npm run start` - Запуск продакшен сервера
- `npm run lint` - Запуск ESLint

## Проверка продакшн версии

Чтобы проверить работу приложения в продакшн режиме локально:

1. Установите переменную окружения:

```env
NODE_ENV=production
```

2. Соберите приложение:

```bash
npm run build
```

3. Запустите продакшн сервер:

```bash
npm run start
```

4. Откройте [http://localhost:3000](http://localhost:3000) в браузере

Что проверить:
- ✓ Все переменные окружения корректно загружаются
- ✓ Поиск работает с обоими провайдерами (Exa.ai и Serper)
- ✓ Суммаризация работает с выбранной моделью OpenAI
- ✓ Все режимы поиска функционируют правильно
- ✓ Темная/светлая тема переключается
- ✓ Источники корректно отображаются
- ✓ Follow-up вопросы работают

### Отладка продакшн версии

Если возникли проблемы:

1. Проверьте логи сборки:

```bash
npm run build
# Смотрите на наличие ошибок в выводе
```

2. Включите режим отладки:

```env
NEXT_PUBLIC_DEBUG=true
```

3. Проверьте логи сервера:

```bash
npm run start
# Следите за выводом в консоли
```

4. Проверьте консоль браузера на наличие ошибок

### Известные проблемы

1. Rate Limiting:
   - OpenAI API имеет ограничения на запросы
   - Exa.ai и Serper также имеют лимиты
   - В продакшене рекомендуется настроить кэширование

2. Переменные окружения:
   - Убедитесь, что все NEXT_PUBLIC_ переменные доступны на клиенте
   - Серверные переменные (OPENAI_API_KEY) должны быть установлены на серв��ре

3. CORS и прокси:
   - При развертывании убедитесь, что все API endpoints доступны
   - Возможно потребуется настройка CORS или прокси

## Запуск в Docker

### Локальный запуск

1. Создайте файл `.env.production` на основе `.env.example`:

```bash
cp .env.example .env.production
```

2. Отредактируйте `.env.production`, установив все необходимые переменные окружения.

3. Соберите и запустите контейнер:

```bash
docker-compose up --build
```

4. Приложение будет доступно по адресу [http://localhost:3000](http://localhost:3000)

### Развертывание на сервере

1. Подготовьте сервер:

```bash
# Установите Docker и docker-compose
sudo apt update
sudo apt install docker.io docker-compose
```

2. Скопируйте файлы на сервер:

```bash
# Создайте директорию для проекта
ssh user@your-server "mkdir -p /path/to/app"

# Скопируйте файлы
scp docker-compose.yml Dockerfile .env.production user@your-server:/path/to/app/
```

3. Подключитесь к серверу и запустите приложение:

```bash
ssh user@your-server
cd /path/to/app
docker-compose up -d
```

### Управление контейнером

- Просмотр логов:

```bash
docker-compose logs -f
```

- Перезапуск приложения:

```bash
docker-compose restart
```

- Остановка приложения:

```bash
docker-compose down
```

- Обновление до новой версии:

```bash
git pull  # получаем новую версию кода
docker-compose down  # останавливаем текущий контейнер
docker-compose up --build -d  # собираем и запускаем новую версию
```

### Мониторинг

- Проверка статуса:

```bash
docker-compose ps
```

- Проверка использования ресурсов:

```bash
docker stats
```

- Проверка логов приложения:

```bash
docker-compose logs -f app
```

### Рекомендации по безопасности

1. Переменные окружения:
   - Не храните чувствительные данные в репозитории
   - Используйте `.env.production` для продакшн окружения
   - Регулярно обновляйте API ключи

2. Сеть:
   - Используйте HTTPS прокси (например, Nginx) перед контейнером
   - Настройте файрвол на сервере
   - Ограничьте доступ к портам

3. Обновления:
   - Регулярно обновляйте базовый образ Node.js
   - Следите за обновлениями зависимостей
   - Используйте фиксированные версии в package.json

## Используемые технологии

- Next.js 14
- React 18
- TypeScript
- Tailwind CSS
- shadcn/ui
- OpenAI GPT-4
- Exa.ai Search API
- TanStack Query
- Lucide Icons 