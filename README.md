# tb
#List the required librares
import telebot
from telebot import types

#withdraw token
token = '1745520593:AAEeIyHti0K27FMMB2kSlcueRD1fP2Q-Knw'
bot = telebot.TeleBot(token)

#creating buttons
keyboard = telebot.types.ReplyKeyboardMarkup(True)
keyboard.row('/Asia', '/Arctic', '/Europe')
keyboard.row('/NorthAmerica', '/Oceania', '/SouthAmerica')
keyboard.row('/Wildfire')

@bot.message_handler(commands=['Asia'])
def start(message):
    markup = types.InlineKeyboardMarkup()
    markup.add(types.InlineKeyboardButton('Learn more about wildfire by country', url='https://en.wikipedia.org/wiki/List_of_wildfires#Asia'))
    bot.send_message(message.chat.id,
                     'Asia is the largest part of the world, both in terms of territory, population and density.',
                     parse_mode='html', reply_markup=markup)

@bot.message_handler(commands=['Arctic'])
def start(message):
    markup = types.InlineKeyboardMarkup()
    markup.add(types.InlineKeyboardButton('More detailed', url='https://www.bbc.com/news/world-europe-49125391'))
    bot.send_message(message.chat.id,
                    'According to the WTO in June 2019 arctic wildfires emitted 50 megatonnes of CO2. This was more than between 2010 and 2018 combined. Most carbon release was from Alaska and Siberia, but also included other arctic areas e.g. in Alberta. In Siberia temperature was about 10C higher in June 2019 than the average. In Anchorage, Alaska, on 4 July 2019, the temperature was 32C (90F), setting a new all-time record high temperature for the town.',
                    parse_mode='html', reply_markup=markup)

@bot.message_handler(commands=['Europe'])
def start(message):
    markup = types.InlineKeyboardMarkup()
    markup.add(types.InlineKeyboardButton('Learn more about wildfire by country', url='https://en.wikipedia.org/wiki/List_of_wildfires#Europe'))
    bot.send_message(message.chat.id,
                     'More European countries suffered from large forest fires in 2018 than ever before, and Sweden experienced the worst fire season in reporting .',
                     parse_mode='html', reply_markup=markup)

@bot.message_handler(commands=['NorthAmerica'])
def start(message):
    markup = types.InlineKeyboardMarkup()
    markup.add(types.InlineKeyboardButton('Learn more about wildfire by country', url='https://en.wikipedia.org/wiki/List_of_wildfires#North_America'))
    bot.send_message(message.chat.id,
                     'From 2007 to 2017, wildfires burned an average of 6.2 and 6.6 million acres/year in the U.S. and Canada, respectively.',
                     parse_mode='html', reply_markup=markup)

@bot.message_handler(commands=['Oceania'])
def start(message):
    markup = types.InlineKeyboardMarkup()
    markup.add(types.InlineKeyboardButton('More detailed', url='https://en.wikipedia.org/wiki/List_of_wildfires#Oceania'))
    bot.send_message(message.chat.id,
                     'Wildfires in Australia and New Zealand.',
                     parse_mode='html', reply_markup=markup)

@bot.message_handler(commands=['SouthAmerica'])
def start(message):
    markup = types.InlineKeyboardMarkup()
    markup.add(types.InlineKeyboardButton('Learn more about wildfire by country', url='https://en.wikipedia.org/wiki/List_of_wildfires#South_America'))
    bot.send_message(message.chat.id,
                     'Wildfires in South America.',
                     parse_mode='html', reply_markup=markup)

@bot.message_handler(commands=['Wildfire'])
def open_website(message):
    markup = types.InlineKeyboardMarkup()
    markup.add(types.InlineKeyboardButton('MORE DETAILED', url='https://en.m.wikipedia.org/wiki/List_of_wildfires'))
    bot.send_message(message.chat.id,
                     'A wildfire, bushfire, wildland fire or rural fire is an unplanned, unwanted, uncontrolled fire in an area of combustible vegetation starting in rural areas and urban areas.',
                     parse_mode='html', reply_markup=markup)

def send(id, text):
    bot.send_message(id,text, reply_markup= keyboard)

@bot.message_handler(commands = ['start'])
def answer(message):
    send(message.chat.id, 'Hello! I am very glad that you have contacted me. Please select the question you are interested in.'
                          'If you want to see a real forest fire forecast. Then follow this link: https://colab.research.google.com/drive/1SyARj_8-yP6m5rlFV3cQIZFJ58bAXc6b#scrollTo=GPdOYFL90XJz ( the forecast belongs to the region of Portugal ).')

@bot.message_handler(content_types= ['text'])
def main(message):
    id = message.chat.id
    msg = message.text

    if msg == 'Hello':
        send(id, 'Hello!')
    else:
        send(id, 'Error')
#If the user displays the wrong word, then the bot generates an error

bot.polling(none_stop= True)
