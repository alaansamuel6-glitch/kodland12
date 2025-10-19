from telebot import TeleBot
from telebot.types import (
    ReplyKeyboardMarkup, 
    KeyboardButton, 
    WebAppInfo,
    InlineKeyboardMarkup,
    InlineKeyboardButton
)

BOT_TOKEN = "8144846739:AAGR7noz3r_3k8hBZmUSYWy_KY2-w_zXcsQ" 
WEB_URL = "https://yandex.ru/games/app/351956" 

bot = TeleBot(BOT_TOKEN)

@bot.message_handler(commands=["start"])
def start(message):
    reply_keyboard_markup = ReplyKeyboardMarkup(resize_keyboard=True)
    reply_keyboard_markup.row(KeyboardButton("Запустить homakweb", web_app=WebAppInfo(WEB_URL)))
    inline_keyboard_markup = InlineKeyboardMarkup()
    inline_keyboard_markup.row(InlineKeyboardButton('Запустить homakweb', web_app=WebAppInfo(WEB_URL)))
    bot.reply_to(message, "Нажмите на кнопку ниже, чтобы запустить homakweb", reply_markup=inline_keyboard_markup)
    bot.reply_to(message, "Нажмите на кнопку клавиатуры, чтобы запустить homakweb", reply_markup=reply_keyboard_markup)
@bot.message_handler(content_types=['web_app_data'])
def web_app(message):
    bot.reply_to(message, f'Ваше сообщение: "{message.web_app_data.data}"')

bot.infinity_polling()
