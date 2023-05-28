# Genesis_case

План виконання завдання
Для реалізації цього сервісу з АРІ, потрібно виконати кілька кроків. Ось загальний план, який можна використати для цієї задачі:

Встановлення зв'язку з АРІ для отримання поточного курсу біткоіна (BTC) у гривні (UAH). Для цього можна використати публічне АРІ, наприклад, таке як CoinGecko або CoinMarketCap. Зареєструйтесь на відповідному сайті, отримайте ключ АРІ та дізнайтесь, як отримати поточний курс біткоїна.

Реалізуйте функцію, яка буде отримувати поточний курс біткоіна з використанням отриманого ключа АРІ. Ця функція повинна робити запит до АРІ та повертати поточний курс.

Реалізуйте можливість підписки на отримання інформації про зміну курсу. Створіть базу даних, в якій зберігатимете адреси електронної пошти підписаних користувачів. Додайте функціонал, який дозволить користувачам підписатися на отримання сповіщень про зміну курсу.

Напишіть функцію, яка періодично перевірятиме зміну курсу біткоіна і, у разі його зміни, відправлятиме електронні листи з актуальним курсом всім підписаним користувачам. Для цього використайте бібліотеки або сервіси для відправки електронної пошти, наприклад, SMTP або SendGrid.

Для реалізації пункту 4, який стосується перевірки зміни курсу біткоїна і відправки актуального курсу всім підписаним користувачам, можна створити окремий клас або функцію.
import time
import smtplib
from email.mime.text import MIMEText

class BitcoinRateNotifier:
def **init**(self, api_key):
self.api_key = api_key
self.subscribed_emails = set()

    def check_bitcoin_rate(self):
        # Отримання поточного курсу біткоїна з використанням API та вашого ключа
        current_rate = self.get_current_bitcoin_rate()

        # Перевірка зміни курсу біткоїна

        # Виконання потрібних перевірок
        # Якщо курс змінився, відправляємо сповіщення
        if self.is_rate_changed(current_rate):
            self.send_notifications(current_rate)

    def get_current_bitcoin_rate(self):
        # Логіка для отримання поточного курсу біткоїна з використанням API
        # Використовуйте свій ключ API для зробити запит та отримати поточний курс
        # Повертає поточний курс біткоїна
        # Наприклад:
        # response = make_api_request("https://api.example.com/bitcoin_rate", api_key=self.api_key)
        # current_rate = response['rate']
        # return current_rate
        pass

    def is_rate_changed(self, current_rate):
        # Логіка для перевірки зміни курсу біткоїна
        # Порівняйте поточний курс з попереднім курсом, збереженим в якості стану об'єкту або в базі даних
        # Повертає True, якщо курс змінився, інакше - False
        # Наприклад:
        # previous_rate = self.get_previous_bitcoin_rate() # Отримання попереднього курсу з бази даних або змінної стану
        # return current_rate != previous_rate
        pass

    def send_notifications(self, current_rate):
        # Логіка для відправки сповіщень по електронній пошті
        # Створюємо MIMEText об'єкт з актуальним курсом біткоїна
        message = MIMEText(f"Bitcoin rate has changed. Current rate: {current_rate}")
        message['Subject'] = 'Bitcoin Rate Notification'

        # Відправляємо електронний лист кожному підписаному користувачу
        for email in self.subscribed_emails:
            self.send_email(email, message)

    def send_email(self, recipient, message):
        # Логіка відправки електронного листа через SMTP-сервер
        # Використайте вашу конфігурацію SMTP для відправки листа
        # Наприклад:
        # with smtplib.SMTP('smtp.example.com', 587) as smtp_server:
        #     smtp_server.starttls()
        #     smtp_server.login('your_username', 'your_password')
        #     smtp_server.sendmail('your_email@example.com', recipient, message.as_string())
        pass

    def subscribe_email(self, email):
        # Логіка підписки електронної пошти на отримання сповіщень
        # Додайте адресу електронної пошти до списку підписаних користувачів
        self.subscribed_emails.add(email)

    def unsubscribe_email(self, email):
        # Логіка відписки електронної пошти від отримання сповіщень
        # Видаліть адресу електронної пошти зі списку підписаних користувачів
        self.subscribed_emails.remove(email)

# Приклад використання класу BitcoinRateNotifier

# Створення об'єкту з ключем API

api_key = "your_api_key"
rate_notifier = BitcoinRateNotifier(api_key)

# Підписка на отримання сповіщень

rate_notifier.subscribe_email("example1@example.com")
rate_notifier.subscribe_email("example2@example.com")

# Безкінечний цикл для періодичної перевірки курсу та відправки сповіщень

while True:
rate_notifier.check_bitcoin_rate()
time.sleep(60) # Затримка в секундах між перевірками (60 секунд = 1 хвилина)

# Використання базового образу PHP з веб-сервером Apache

FROM php:7.4-apache

# Встановлення залежностей проекту

COPY composer.json /var/www/html/composer.json
WORKDIR /var/www/html
RUN apt-get update && apt-get install -y \
 unzip \
 && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
 && composer install --no-scripts --no-autoloader

# Копіювання файлів проекту в контейнер

COPY . /var/www/html

# Налаштування веб-сервера Apache

RUN a2enmod rewrite

# Запуск скрипту при старті контейнера

CMD ["apache2-foreground"]
