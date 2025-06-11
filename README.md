# shinobu-bot

import os
from telegram import InlineKeyboardButton, InlineKeyboardMarkup
from telegram.ext import Updater, CommandHandler, CallbackQueryHandler

def start(update, context):
    message = (
        "馃尭 Greetings, honored guest.\n"
        "Welcome to the domain of *Shinobu* 馃.\n\n"
        "_How may I assist you today?_"
    )
    keyboard = [
        [InlineKeyboardButton("馃啌 Free Commands", callback_data='free')],
        [InlineKeyboardButton("馃敁 Premium Features", callback_data='premium')],
        [InlineKeyboardButton("馃柤 Anime Images", callback_data='images'),
         InlineKeyboardButton("馃 Chat with Shinobu", callback_data='chat')],
        [InlineKeyboardButton("馃挸 Subscribe", callback_data='subscribe'),
         InlineKeyboardButton("鈩癸笍 About", callback_data='about')],
    ]
    reply_markup = InlineKeyboardMarkup(keyboard)
    update.message.reply_text(message, reply_markup=reply_markup, parse_mode="Markdown")

def button_handler(update, context):
    query = update.callback_query
    query.answer()
    data = query.data

    if data == 'free':
        query.edit_message_text("馃啌 *Free Commands:*\n`/quote`, `/fact`, `/mission`, `/mood`", parse_mode="Markdown")
    elif data == 'premium':
        query.edit_message_text("馃敁 *Premium Features:*\n`/chat_ai`, `/shinobu_voice`, `/special_mission`, `/image`, `/diary`", parse_mode="Markdown")
    elif data == 'images':
        query.edit_message_text("馃柤 Coming soon: Rare Shinobu anime art and wallpapers!")
    elif data == 'chat':
        query.edit_message_text("馃 Chat feature is available for premium users.\nUse `/chat_ai` after subscribing.")
    elif data == 'subscribe':
        query.edit_message_text("馃挸 *Subscribe to unlock all features!*\nSend /subscribe to start your journey.")
    elif data == 'about':
        query.edit_message_text("鈩癸笍 *About Shinobu Bot:*\nYour personal assistant with the grace of a Hashira.\nInspired by Demon Slayer.")

def main():
    token = os.getenv("BOT_TOKEN")
    updater = Updater(token)
    dp = updater.dispatcher
    dp.add_handler(CommandHandler("start", start))
    dp.add_handler(CallbackQueryHandler(button_handler))
    updater.start_polling()
    updater.idle()

if __name__ == '__main__':
    main()
    
