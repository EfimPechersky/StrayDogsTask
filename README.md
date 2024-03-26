# StrayDogsTask
Задание по Культуре разработки ПО с открытым кодом, связанное с работой с fastapi.

# Описание идеи проекта

На бездомных собак будут надеты умные ошейники, которые будут собирать основную информацию о носителях (геолокация, движение, температура) и передавать её на станцию LoRa, а станция в свою очередь будет передавать полученную информацию на сервер. Информация о бездомных собаках с сервера будет передаваться на приложение через запросы с помощью FastAPI.Пользователи приложения смогут отслеживать местоположение бездомных собак на интерактивной карте и получать информацию о них, а также давать задания другим пользователям (например покормить определённую собаку или проверить её самочуствие) и привязывать свой аккаунт к ошейнику и отвязывать их. Модерация добавляет новые ошейники в систему, проверяет работоспособность установленных ошейников, блокирует пользователей и модерирует приложение.

# Сценарии использования 
1. Регистрация пользователей:
   1) Пользователь вводит логин и пароль дважды. 
   2) Если пароли не различаются приложение отправляет запрос на сервер с данными.
   3) Сервер проверяет данные и отправляет ответ в приложение о правильности или неправильности данных. Если данные правильные, информация о пользователе добавляется в базу данных.
   4) Приложение получает ответ. Если пользователь был добавлен в базу данных то ему открывается доступ к интерфейсу приложения, иначе - уведомляет пользователя об ошибке и просит ввести данные повторно.
2. Регистрация ошейника:
     1) Модератор вводит регистрационный номер устройства и кличку.
     2) Отправляется запрос на сервер.
     3) Сервер проверяет наличие регистрационного номера в базе данных и отправляет результат в обратно. При его отсутствии он добавляет его в базу данных, а при наличии обновляет кличку.
     4) Приложение уведомляет о результате регистрации ошейника.
3. Привязка пользователя к ошейнику:
   1)Пользователь выбирает ошейник доступный к привязке и нажимает кнопку привязать.
   2)Отправляется запрос на сервер.
   3)Сервер проверяет расстояние от пользователя до собаки, и если расстояние меньше максимально допустимого расстояния, то добовляет информяцию о привязке в базу данных, а затем возвращает результат приложению.
   4)Приложение получает ответ и уведомляет пользователя об успешности привязки и обновляет данные о привязке собаки.
4. Удаление привязки:
     1)Пользователь выбирает привязанный ошейник и нажимает кнопку отвязать.
     2) Отправляется запрос на сервер. Сервер удаляет данные о привязке из базы данных.
     3) Приложение получает ответ и уведомляет пользователя об успешной отвязке.
5. Добавление задания:
     1) Пользователь нажимает на кнопку дать задание, далее выбирает доступный ошейник и вид задания.
     2) Отправляется запрос на сервер. Сервер добавляет информацию о задании в базу данных.
     3) Приложение получает ответ и уведомляет пользователя об успешном добавлении задания.
6. Оповещение пользователя о задании:
   1)Каждые 30 минут отправляется запрос на сервер.
   2)Сервер проверяет наличие заданий в базе данных.
   3)Приложение получает ответ и при наличии заданий оповещает пользователя об этом.
7. Отправка отклика на задание:
     1)Пользователь отправляет в качестве отклика на задание фотографию собаки.
     2)Отправляется запрос на сервер. Сервер обновляет статус задания.
8. Верификация задания:
     1)Модератор отправляет результат верификации.
     2)Отправляется запрос на сервер. Сервер обновляет статус задания.
9. Вход пользователя:
   1) Пользователь вводит логин и пароль. 
   3) Сервер проверяет данные и отправляет ответ в приложение о правильности или неправильности данных.
   4) Приложение получает ответ. Если данные правильные то ему открывается доступ к интерфейсу приложения, иначе - уведомляет пользователя об ошибке и просит ввести данные повторно.
# Запросы
# Собаки
|Название запроса|Метод|Тело|Ответ|
|----------------|-----|----|-----|
|Регистрация ошейника |POST|Регистрационный номер, Кличка|ID(int)|
|Получение списка ошейников|GET||JSON(list)|
|Отправка координат|POST|ID, широта, долгота, время|Status|
|Получение трека|GET|ID,Начальное время|UID(int)|

   

