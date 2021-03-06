# Начало работы с vkwave

![vkwave](https://user-images.githubusercontent.com/28061158/75329873-7f738200-5891-11ea-9565-fd117ea4fc9e.jpg)

В этом уроке мы сделаем следующее:
+ [Установим библиотеку](#Установка-библиотеки)
+ [Напишем простейшего echo бота](#Простейший-echo-бот)

# Установка библиотеки

Для установки vkwave вам понадобится [python](https://www.python.org/downloads/ "Ссылка для на официальный сайт Python")

Итак, установить vkwave можно с PyPi и Github.
Если вы не гонитесь за новыми функциями, ставьте с PyPi.
В противном случае ставьте с Github.

Установка с PyPi:
```
pip install vkwave
```
Установка с GitHub:
```
pip install https://github.com/fscdev/vkwave/archive/master.zip
```

# Простейший echo бот

Echo бот — самая простая задача, он возвращает отправленное ему сообщение, например: вы написали ему: "Привет", бот ответит "Привет"

Итак, перейдём к коду:
```python
# Обратите внимание, версия лонгпула должна быть больше или равна 5.103
TOKEN = "Сюда токен"
GROUP_ID = 123456

# Импортируем нужные классы.
# SimpleLongPollBot: обёртка для более удобной работы с фреймворком
# SimpleBotEvent: тип события, который предоставляет SimpleLongPollBot
from vkwave.bots import SimpleLongPollBot, SimpleBotEvent

# инициализируем бота (можно ввести список токенов, тогда vkwave сможет обходить лимиты ВКонтакте)
bot = SimpleLongPollBot(tokens=TOKEN, group_id=GROUP_ID)

# декоратор для создания обработчиков.
# можно передавать свои фильтры, но в данном случае мы хотим принимать все сообщения
@bot.message_handler()
def echo(event: SimpleBotEvent) -> str:
    # мы можем сразу возвращать текст, т.к vkwave понимает, что если вы возвращаете строку, то вы хотите ответить на сообщение этим текстом. пользователь может задать свои типы данных, которые он сможет возвращать из хендлеров (а также написать нужную логику для их преобразования в нужные действия)
    return event.object.object.message.text

# запускаем бота с игнорированием ошибок (не останавливаться даже при них)
bot.run_forever()
```

На этом первый урок закончен. Удачи!