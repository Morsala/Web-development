# PHP и XAMPP

## Работа с XAMPP

Перед началом работы сначала скачайте [XAMPP](https://www.apachefriends.org)

!!! Запомните путь установки XAMPP, либо сами задайте путь при установке

После установки, запустите приложение `XAMPP Control Panel`

![image](https://user-images.githubusercontent.com/47351812/205981359-c2d750dd-ab09-434e-8e46-95449d942e59.png)

Нажмите кнопку `start` напротив `Apache` и `MySQL`

![image](https://user-images.githubusercontent.com/47351812/205981613-34fbc161-149c-46db-92af-ad45036bbcea.png)

Чтобы проверить работу `XAMPP`, в адресной строке браузера введите `localhost`

![image](https://user-images.githubusercontent.com/47351812/205981918-3e827de4-37cc-4efc-9d26-af4f7d6c8b01.png)

Далее создайте папку в `путь_установки_XAMPP/htdocs/`. В ней будет лежать ваш проект. `XAMPP` работает с файлами расширения `.php`

Чтобы запусть данный проект введите в адресную строку браузера `localhost/название_проекта`

## Работа с phpMyAdmin

Чтобы работать с базой данных, нужно сначала ее создать)

Итак, заходим в `localhost`, затем нажимаем сверху на раздел `phpMyAdmin`

![image](https://user-images.githubusercontent.com/47351812/205983218-de7e853a-5fec-49eb-a178-d66007c764d6.png)

Открывается страница управления баз данных MySQL

![image](https://user-images.githubusercontent.com/47351812/205983375-47d0c67c-0df5-4735-90a6-82bfa89777c6.png)

Создаем базу данных:

1. Нажимаем на кнопку слева `Создать БД`

![image](https://user-images.githubusercontent.com/47351812/205983501-e9cdcdc4-d2e9-466b-8e91-5e6d40e991a4.png)

2. Пишем нужное имя базы данных и нажимаем на кнопку `Создать`
3. Указываем название таблицы, количество столбцов и нажимаем `Создать`
4. Заполняем нужные поля (пример показан на скрине)

![image](https://user-images.githubusercontent.com/47351812/205985927-cee5e907-1ba0-42de-9945-965e32b3bbcc.png)

5. Пролистываем вниз и нажимаем кнопку `Сохранить`

Все, база данных готова)

## Домашнее задание

1. Сверстать 3 страницы: Авторизация, Регистрация, Список дел (Пример на скринах)

![image](https://user-images.githubusercontent.com/47351812/217252081-65a5133d-c3e5-45d5-a4af-6c8e9ec95660.png)
![image](https://user-images.githubusercontent.com/47351812/217252192-be11ead9-c310-46b8-9a7d-3aecd588f174.png)
![image](https://user-images.githubusercontent.com/47351812/217252400-f278ac5e-0ee7-4e99-a30a-2fe601431b22.png)

3. Прочитать про синтаксис `php` [здесь](https://metanit.com/php/tutorial/) и [здесь](https://php.net)
4. Написать на `php` вывод содержимого всех полей `input`
