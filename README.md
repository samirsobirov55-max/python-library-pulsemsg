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

bot = Bot(token="ВАШ_ТОКЕН", base_url="https://www.pulsemessenger.space") # <<НЕ МЕНЯТЬ base_url!!
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


## 🔌 Bot API

Pulse поддерживает Bot API совместимый с Telegram по структуре.

Базовый URL: `https://www.pulsemessenger.space/api/bot/:token/`

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
