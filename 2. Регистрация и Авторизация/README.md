# Регистрация и Авторизация

Код `php` можно использовать в любом месте верстки при условии, что сама верстка лежит в файле с расширением `.php`

Чтобы вставить код `php` в верстку необходимо использовать специальный тег `<?php ... ?>`, где `...` сам код. Например:

    <?php
       echo "Hello, world";
    ?>
    
Теперь вернемся к Регистации и Авторизации

## Подключение к базе данных

Подключение к базе данных в `phpMyAdmin` можно осущствлять несколькими способами: встроенными методами или специальными классами. Мы будешь использовать специальный класс `PDO`, который упрощает взаимодействие с баззой данных.

Для подключения к базе данных, нужно создать экземпляр класса и заполнить в конструкторе класса необходимые поля, а именно:

1. `ServerName` - имя сервера (так как мы используем локальную сеть с помощью `xampp`, она будет иметь значение `localhost`);
2. `dbName` - имя базы данных (здесь вы вставляете имя базы данных, которую создавали в `phpMyAdmin`);
3. `UserName` - логин пользователя в вашей сети (по умолчанию в `xampp` используется имя пользователя `root`);
4. `Password` - пароль вашего пользователя в сети (по умолчанию оставляем пустым);

Теперь вставляем все данные в конструктор `PDO`:

![image](https://user-images.githubusercontent.com/47351812/229349097-952ffc37-bb88-458a-b282-4257c5795320.png)

`Важно! Для удобства перенесите подключение к базе данных в отдельный файл (например config.php) и, при взаимодействии с базой данных, просто подключайте данный файл через require "config.php"; Таким образом, подключение к базе данных у вас будет в одном месте и, при необходимости, вам нужно будет поменять код только в одном месте.`

## Регистрация

Дальше делаем регистрацию. Для этого необходимо выполнить следующие шаги:

1. Получить данные пользователя через тег `form` для выполнения регистрации;
2. Подключиться к базе данных;
3. Подготовить шаблон запроса к базе данных на выполнении регистрации;
4. Выполнить запрос, отправив в шаблон необходимые данные
5. Проверить таблицу в базе данных на заполнение данными пользователя.

### Получение данных у пользователя

Для получения данных пользователя в верстке необходимо использовать тег `form` и соответствующие поля `input`:

![image](https://user-images.githubusercontent.com/47351812/229350818-c6cb0b9a-a8ee-43a8-bd25-abe3584ecb45.png)

Для получения данных с полей `input` нужно выполнить следующие условия:

1. В теге `form` обязателен атрибут `method`, в котором должно лежать значение `post`;
2. Кнопка Регистрации обязательно должна быть тегом `input` с атрибутом `type="submit" (иначе кнопка нажиматься не будет)`;
3. У каждого тега `input` должен быть атрибут `name`, которому вы будете обращаться в коде Регистрации;
4. Если вы хотите писать код не в данном файле, а в отдельном для убоства можно использовать в теге `form` атрибут `action="путь к испольняемому файлу.php"`;

В данном случае мы писали код в самом файле верстки, поэтому атрибут `action` не использовался.

Далее, чтобы обработать собитие нажатия на кнопку используем метод `post`, прописанный в теге `form` `(для тех, кто пишет код в отдельном файле эту проверку писать не надо)`:

![image](https://user-images.githubusercontent.com/47351812/229350830-c777cd92-2822-48fe-9305-3d882f55568e.png)

- Метод `isset()` позволяет проверить, менялось ли значение у поля (в данном случае нажата ли кнопка)
- Переменная `$_POST` является списком обьектов типа `ключ-значение`, в котором находятся все `input` в данной форме
- `registr` это `name` кнопки Регистрации

После того, как мы отловили нажатие на кнопку Регистрации, получаем данные с полей, введеные пользователем:

![image](https://user-images.githubusercontent.com/47351812/229350232-8ff61dec-a59b-495d-8b89-c82e0e9d1dc7.png)

Здесь все также используем переменную `$_POST` и `name` полей для получения данных 

### Подключение к базе данных

Подключение к базе данных мы осуществили в прошлый раз, поэтому просто используем подключение нашего файла `config.php`:

![image](https://user-images.githubusercontent.com/47351812/229350337-695b7976-5ce2-4122-ae60-cd1b7ee9c393.png)

### Подготовка шаблона запроса к базе данных на выполнении регистрации

В данном проете мы будем использовать четыре вида запроса в базу данных:

- `SELECT` - получить данные из таблицы
- `INSERT` - записать данные в таблицу
- `UPDATE` - изменить данные в таблице
- `DELETE` - удалить данные из таблицы

Для регистрации очевидно нужно использовать запрос на добавление данных `INSERT`.

Для получения шаблона данного запроса можно зайти в вашу таблицу в `phpMyAdmin` и выбрать раздел `SQL`

![image](https://user-images.githubusercontent.com/47351812/229350641-74690f45-2cc8-47e4-afbf-f4586458b378.png)

Копируем данную строчку, убираем все одинарные кавычки и подставляем вместо [value-1] знаки `?`:

![image](https://user-images.githubusercontent.com/47351812/229350762-242655c9-fc2c-4355-9703-b1e9a5fd3cf4.png)

Вместо знаков `?` мы потом поставим наши данные.

### Отправляем запрос в базу данных

Мы создали запрос на добавление данных. Следующим шагом у нас будет отправить его в базу данных с использованием данных пользователя. Это делается следующим образом:

![image](https://user-images.githubusercontent.com/47351812/229350994-1dceffe0-c6f6-4629-9819-c1a3aad3d761.png)

- `$result` это переменная, которая будет содержать ответ от базы данных (Успешно или Неуспешно);
- `$pdo->prepare($request)` - подготавливает запрос для его отправки;
- `$result->execute([])` -подставляет данные вместо знаков `?` (обратите внимание на то, что отправка происходит в массиве. Количество переменных в массиве должно быть равным количеству знаков `?` в запросе);

### Проверяем, успешно ли выполнился запрос

Для проверки запроса `INSERT` нам нужно всего лишь проверить что содержится в переменной `$result` - `true` или `false`:

![image](https://user-images.githubusercontent.com/47351812/229351219-2fa71e18-b35d-41e7-b679-ab16eb530455.png)

- `header("Location: ...")` перенаправляет нас на другую страницу (в данном случае на страницу входа).

Также можно посмотреть данные в нашей таблице в `phpMyAdmin`

![image](https://user-images.githubusercontent.com/47351812/229351299-5ccc1e0b-2811-47b5-9e23-105e4c25bdd7.png)

Целиком код будет выглядеть следующим образом:

![image](https://user-images.githubusercontent.com/47351812/229351355-8a3bd527-d13f-473d-a493-4352cd14d866.png)

## Авторизация

Авторизация происходит точно по такому же сценарию, как и Регистрация. Только запрос в данном случае будет не на добавление данных, а на получение их из таблицы.

Единственное, что будет меняться - сам запрос. Он будет иметь следующий вид: 

![image](https://user-images.githubusercontent.com/47351812/229351460-1b45ee44-778e-45ec-ab94-f20a61b2db64.png)

Приписка `WHERE` - это условия выборки данных. В данном случае мы получаем пользователя, где логин и пароль такие же, как и ввел пользователь.

Здесь переменная `$result` будет содержать полученные данные из таблицы. Они имеют вид списка, поэтому чтобы проверить, что данный пользователь существует, ножно просто проверить, что запись в списке присутствует:

![image](https://user-images.githubusercontent.com/47351812/229351636-6fc59e61-31e8-4451-9df9-b316037341cf.png)

Здесь мы используем метод `$result->fetch()`, который вытаскивает из списка очередную строку. И, если она не пустая, то такой пользователь найден.

В итоге код Авторизации будет иметь следующий вид:

![image](https://user-images.githubusercontent.com/47351812/229351726-626fbb27-db9a-49e1-ada7-65107238c4d5.png)

`todo.php` - страница с нашим списком дел

## Задание

Написать в своем проекте Регистрацию и Авторизацию пользователя.
