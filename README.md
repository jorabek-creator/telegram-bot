from aiogram import Bot, Dispatcher, types
from aiogram.types import ReplyKeyboardMarkup, KeyboardButton
from aiogram.utils import executor
import logging
import os

# Token va admin username
BOT_TOKEN = os.getenv(7460023349:AAGpz7D72U5mFavRcTDC-lu3zlJaxSPRX4w)
ADMIN_USERNAME = os.getenv(@Khudayarov_08_17)

# Log
logging.basicConfig(level=logging.INFO)

# Bot va dispatcher
bot = Bot(token=BOT_TOKEN)
dp = Dispatcher(bot)

# Asosiy menyu tugmasi
main_kb = ReplyKeyboardMarkup(resize_keyboard=True)
main_kb.add(KeyboardButton("🛍 Buyurtma berish"))

# /start komandasi
dp.message_handler(commands=['start'])(
    lambda message: message.answer(
        "Assalomu alaykum! Qanday yordam bera olaman?",
        reply_markup=main_kb
    )
)

# Buyurtma tugmasi
dp.message_handler(lambda message: message.text == "🛍 Buyurtma berish")(
    lambda message: message.answer(
        f"Buyurtma berish uchun adminga murojaat qiling: @{ADMIN_USERNAME}"
    )
)

# Kanalga post chiqsa userlarga yuborish uchun webhook kerak bo'ladi
# Bunda admin kanalga post chiqarganda bot xabar yubora olmaydi,
# lekin bu imkonni bot API orqali emas, server orqali qilish mumkin

if __name__ == '__main__':
    executor.start_polling(dp)
