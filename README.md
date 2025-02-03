## Avito Parser v.2.1.1

Последние исправление в версии 2.1.1:
- Исправлены следующие известные баги:
1) Баг связанный с ограничением по количеству просмотров
2) Баг с ключевыми словами (белый и черный список), если он состоял из выражения, например "черный iphone"
3) Ошибка Javascript
4) Зависание парсера если нажать кнопку "Стоп" во время паузы
5) Лишние пробелы в entrypoint.sh
6) Баг при использовании прокси на Linux в безголовом режиме
7) Парсер не пропускал уже просмотренные объявления
- Добавлена возможность парсинга объявлений в профиле продавца (раньше парсер не видел эти объявления)


### Возможности

- Удобное управление с помощью графического интерфейса
- Кроссплатформенность
- Поддержка до 50 ссылок для отслеживания
- Поддержка прокси
- Постоянная проверка новых объявлений
- Установка количества проверяемых страниц
- Установка паузы между повторами
- Уведомление в telegram как опция (может быть несколько получателей), также результат сохраняется в result/keyword*.xlsx и выводится в окно
- Хранение уже просмотренных объявлений, т.е. дубли игнорируются (если на них не поменялась цена)
- Обнаружения изменения цены для уже просмотренных объявлений
- Автоматический обход бана по IP со стороны Авито
- Присылает только объявления, которые подходят под нужные параметры (слова-ключи, стоп-слова, гео, цена, макс. кол-во просмотров), если они указаны конечно
- Несколько режимов работы и запуска
- Возможность запускать на сервере (без браузера и графического интерфейса)

### Обзор возможностей и другие детали:
[youtube](https://youtu.be/q3BlBiLId40) - обзор последней версии, настоятельно рекомендую посмотреть

[youtube](https://youtu.be/CjFQ8zCG1Z0) - подробная инструкция как это всё запустить на удаленном сервере (vps без докера)

[youtube playlist](https://www.youtube.com/playlist?list=PLK9kK8z0fpqxPakGZvxo7y6HtCBTYihUF) - плейлист о том, как это создавалось

### Прокси

Для полноценного использования необходимо использовать мобильные прокси, хорошие можно купить [по ссылке](https://mobileproxy.space/?p=92286).  Вот купон на скидку 20%: eMy-r4y-FZE-kMu

При покупке обязательно выбирайте страну "Россия", остальное на своё усмотрение.

### Установка
Если Ваша платформа - Windows 10 или 11, можете использовать портативную версию [скачать](https://disk.yandex.by/d/dwLd3y3hX1gtig) (обновлено 04.02.2025), распаковать архив, запустить parse_avito.exe от имени администратора). Первый запуск может длиться около 1 минуты - это нормально. В этом случае никаких зависимостей устанавливать не нужно, просто пользуйтесь.


Для работы требуется Python 3.11+. Скопируйте проект и установите зависимости:

```bash
  pip install -r requirements.txt
```

Если Вы будете запускать с графическим интерфейсом, то дополнительно установите Flet (возможно появиться сообщение о конфликте версий, но работать будет)

```bash
  pip install flet
```

У Вас также должен быть установлен браузер Google Chrome любой более менее свежей версии

Запустите **AvitoParser.py** (режим с графическим интерфейсом)

```bash
  python AvitoParser.py
```

Если Вам необходимо запустить парсер на сервере (режим без графического интерфейса), запускайте:

```bash
  python parser_cls.py
```

#### Если Вам необходимо получать уведомления о новых объявлениях в telegram - Вам нужен token и chat_id. Чтобы их получить:

- Перейдите в диалог с **https://t.me/BotFather**
- Введите команду **/newbot**, придумайте name и username для бота
- Скопируйте token и вставьте в Avito Parser в нужное поле
- Перейдите в диалог с Вашим ботом по ссылке из прошлого шага, ссылка имеет формат: **t.me/your_bot**
- Напишите **@get_id_bot** и скопируйте **chat_id** вашего диалога, вставьте его во второе поле данного скрипта
- Можно указать несколько **chat_id**, в таком случае сообщения будут получать несколько человек
- При нажатии на кнопку Test в скрипте, Вам должно прийти сообщение. Если нет, перезагрузите скрипт и попробуйте еще раз


### Docker
```bash
  sudo docker build -t avito_parser:v0.1 .
```
```bash
sudo docker run -it -e URL_AVITO="https://www.avito.ru/all?q=kawasaki+1000sx https://www.avito.ru/all?q=kawasaki+ninja+1000" -e TG_TOKEN="XXXXXXXXXX:XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" -e CHAT_ID_TG="-XXXXXXXXXX" -e FAST_SPEED_AVITO=250 -e MAX_VIEW_AVITO=4 -e MIN_PRICE_AVITO=700000 -e KEYS_AVITO="" --mount type=bind,source=/home/alex/AvitoDataKava,destination=/parse_avito/result avito_parser:v0.1 avito

```


### Проблемы

При обнаружении ошибок, пишите в https://github.com/Duff89/parser_avito/issues.
Пожалуйста, указывайте не только ошибку, но и информацию о Вашей ОС, версию скрипта, способ запуска и т.д.
Для прямой связи с автором, пишите: sergeichopolovich1989@gmail.com. 
Письма на почту с текстом: "у меня не запускается" будут игнорироваться, для этого есть issues


### Поддержка развития проекта

Ваша поддержка очень важна для дальнейшего и регулярного развития данного скрипта.
Поддержать можно по ссылке: https://yoomoney.ru/to/410014382689862
или простым переводом 2204 1201 0103 5539. Заранее спасибо
