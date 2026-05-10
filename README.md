<div align="center">

<img src="client/public/icon.svg" width="80" alt="Pulse logo"/>

# ⚡ Pulse Messenger

**Полнофункциональный мессенджер с Glassmorphism-дизайном и поддержкой ботов**

[![MIT License](https://img.shields.io/badge/license-MIT-7C5CFC?style=flat-square)](LICENSE)
[![Node.js](https://img.shields.io/badge/Node.js-18+-339933?style=flat-square&logo=node.js)](https://nodejs.org)
[![React](https://img.shields.io/badge/React-18-61DAFB?style=flat-square&logo=react)](https://react.dev)
[![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-47A248?style=flat-square&logo=mongodb)](https://mongodb.com)
[![PyPI](https://img.shields.io/pypi/v/pulsemsg?style=flat-square&label=pulsemsg&color=7C5CFC)](https://pypi.org/project/pulsemsg/)

[Демо](#) · [SDK для ботов](https://pypi.org/project/pulsemsg/) · [Документация](#структура-проекта)

</div>

---

## ✨ Возможности

- 💬 **Личные и групповые чаты** — приватные сообщения, группы, каналы
- 🤖 **Система ботов** — BotFather для создания ботов, полноценный Bot API
- 📎 **Медиа** — изображения, видео, голосовые, файлы до 4 ГБ (Premium)
- 🎙 **Звонки** — WebRTC голосовые и видеозвонки
- ⭐ **Звёзды** — внутренняя валюта, платные реакции
- 🎁 **Подарки** — анимированные подарки между пользователями
- 📁 **Папки** — организация чатов по папкам
- 🎨 **Стикеры** — создание и отправка стикер-паков
- 🌙 **Glassmorphism UI** — тёмная тема с размытым стеклянным эффектом
- 📱 **Кроссплатформенность** — веб, Electron (desktop), Capacitor (Android/iOS)

---

## 🤖 Python SDK для ботов

Создавай ботов для Pulse как на aiogram — через библиотеку **[pulsemsg](https://pypi.org/project/pulsemsg/)**:

```bash
pip install pulsemsg
```

```python
from pulsemsg import Bot, Dispatcher, F, Command, run_polling
from pulsemsg.types import Message, InlineKeyboardMarkup, InlineKeyboardButton

bot = Bot(token="ВАШ_ТОКЕН", base_url="https://auragram-telegram-web.hf.space")
dp  = Dispatcher()

@dp.message(Command("start"))
async def start(msg: Message):
    kb = InlineKeyboardMarkup(inline_keyboard=[
        [InlineKeyboardButton("👋 Привет!", callback_data="hello")],
    ])
    await msg.answer("Выбери действие:", reply_markup=kb)

@dp.message()
async def echo(msg: Message):
    await msg.reply(f"🔁 {msg.text}")

if __name__ == "__main__":
    run_polling(dp, bot)
```

Токен получи у `@botfather` внутри Pulse. Подробнее: [pypi.org/project/pulsemsg](https://pypi.org/project/pulsemsg/)

---

## 🛠 Стек технологий

| Часть | Технологии |
|---|---|
| **Клиент** | React 18, Vite, Socket.IO, Axios |
| **Сервер** | Node.js, Express, Socket.IO, JWT, Multer |
| **База данных** | MongoDB (Mongoose) |
| **Деплой** | Docker, Hugging Face Spaces |
| **Мобильный** | Capacitor (Android / iOS) |
| **Desktop** | Electron |
| **Bot SDK** | Python / pulsemsg |

---

## 📁 Структура проекта

```
pulse/
├── client/                   # React-приложение
│   ├── src/
│   │   ├── components/
│   │   │   ├── ChatWindow.jsx      # Основное окно чата
│   │   │   ├── Sidebar.jsx         # Боковая панель / список чатов
│   │   │   ├── InlineKeyboard.jsx  # Inline-кнопки ботов
│   │   │   ├── Profile.jsx         # Профиль пользователя
│   │   │   ├── Settings.jsx        # Настройки
│   │   │   └── ...
│   │   ├── contexts/               # AuthContext, SocketContext
│   │   └── pages/                  # AuthPage
│   └── electron/                   # Desktop-обёртка
│
├── server/                   # Express-сервер
│   ├── models/
│   │   ├── User.js                 # Пользователь (+ isBot)
│   │   ├── Chat.js                 # Чат и сообщения
│   │   ├── Bot.js                  # Модель бота
│   │   └── BotUpdate.js            # Очередь апдейтов для ботов
│   ├── routes/
│   │   ├── auth.js                 # Регистрация / вход
│   │   ├── messages.js             # Сообщения
│   │   ├── chats.js                # Управление чатами
│   │   ├── bots.js                 # Bot API (/api/bot/:token/...)
│   │   └── ...
│   ├── socket/index.js             # WebSocket (Socket.IO)
│   └── utils/
│       ├── botFather.js            # BotFather — создание ботов
│       ├── supportBot.js           # Бот поддержки
│       └── stickerBot.js           # Стикер-бот
│
└── docker-compose.yml
```

---

## 🚀 Быстрый запуск

### Требования

- Node.js 18+
- MongoDB (локально или [Atlas](https://mongodb.com/atlas))
- npm / yarn

### 1. Клонируй репозиторий

```bash
git clone https://github.com/ВАШ_ЮЗЕРНЕЙМ/pulse.git
cd pulse
```

### 2. Настрой переменные окружения

```bash
cp server/.env.example server/.env
```

Заполни `server/.env`:

```env
MONGO_URI=mongodb://localhost:27017/pulse
JWT_SECRET=твой_секретный_ключ
PORT=7860
```

### 3. Запусти сервер

```bash
cd server
npm install
npm start
```

### 4. Запусти клиент

```bash
cd client
npm install
npm run dev
```

Открой **[http://localhost:5173](http://localhost:5173)**

---

## 🐳 Запуск через Docker

```bash
docker compose up --build
```

---

## ☁️ Деплой на Hugging Face Spaces

1. Создай новый Space с SDK **Docker**
2. Загрузи файлы репозитория
3. Добавь секреты в настройках Space:

| Ключ | Значение |
|---|---|
| `MONGO_URI` | Строка подключения MongoDB Atlas |
| `JWT_SECRET` | Произвольный секретный ключ |

---

## 🔌 Bot API

Pulse поддерживает Bot API совместимый с Telegram по структуре.

Базовый URL: `https://ваш-сервер.com/api/bot/:token/`

| Метод | Эндпоинт |
|---|---|
| Информация о боте | `GET /getMe` |
| Отправить сообщение | `POST /sendMessage` |
| Редактировать сообщение | `POST /editMessageText` |
| Удалить сообщение | `POST /deleteMessage` |
| Ответить на кнопку | `POST /answerCallbackQuery` |
| Получить апдейты | `POST /getUpdates` |
| Установить webhook | `POST /setWebhook` |
| Статус печатает | `POST /sendChatAction` |

Создавай ботов через `@botfather` прямо в мессенджере.

---

## 📄 Лицензия

MIT © Pulse Team
