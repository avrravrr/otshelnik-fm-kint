## Введение

Это [MU плагин](https://wp-kama.ru/id_3767/must-use-plugins-ili-obyazatelnyie-plaginyi-v-wordpress.html) для WordPress
Позволяет вам дебажить ваши php проекты используя библиотеку [Kint](https://github.com/kint-php/kint)

**Почему не обычный WordPress плагин?**

Предыстория такова:

Мне надоело дебажить через `var_dump($var);` и `print_r($var);`. Хотелось какого-то универсального и более гибкого решения.
Смотрел в сторону Xdebug - но на данный момент мне он кажется избыточным. Так родилась функция `vd($var);` - как аналог var_dump и print_r. Потом она немного расширилась - появился вывод с `die;`, потом появилась для записи в логи сервера. Потом появилась только для вывода данных переменных и объектов видимых админу...
И свой велосипед всегда веселей. Так он поселился в файле functions.php активного ВП шаблона. Но иногда при тестировании я переключал шаблоны - получал конечно проблемы - функции то в других шаблонах нет (там другой functions.php).
Потом это переросло в небольшой ВП плагин - но и тут я иногда натыкался на грабли - плагин бывает отключается в процессе дебага и отладки...
Таким образом я решил оформить это дело в [MU плагин](https://wp-kama.ru/id_3767/must-use-plugins-ili-obyazatelnyie-plaginyi-v-wordpress.html) - этот вид плагинов не отключается никогда.
Создал папку `/wp-content/mu-plugins/` и в корень поместил файлы, а вордпресс автоматически его активирует и никогда не дает его отключить.

Красота.

А недавно я вышел на библиотеку **Kint** - и она мне сильно пригодилась когда приходилось дебажить объекты и массивы.

-----------

## Установка/Обновление

**Установка:**

1. Создайте каталог `mu-plugins` чтобы вышло `/wp-content/mu-plugins/`
2. Скачайте архив этого плагина, распакуйте архив на своем ПК и по FTP залейте туда файл `otshelnik-fm-kint.php` и папку `/ot-fm-kint-resource/`
Получится такая структура:
 ```
    /wp-content/mu-plugins/ot-fm-kint-resource/
    /wp-content/mu-plugins/otshelnik-fm-kint.php
 ```
3. Всё. Работаем и дебажим

**Обновление:**

MU плагины не обновляются средствами вордпресс движка - т.к. они начинают работу раньше этих функций обновлений. Поэтому за обновлениями следите или на гите или в магазине CodeSeller

-----------

## Как работать:
Большинство методов описано на странице библиотеки [Kint](https://github.com/kint-php/kint) и продублировано внутри файла `otshelnik-fm-kint.php`

Я опишу основные возможности ниже. + мои 4-ре функции

`d($var);` - распечатает переменную
`ddd($var);` - распечатает ее и остановит выполнение. Эквивалент `d();die;`
`!d($var);` - сразу отобразит объект/переменную в раскрытом виде
`d(1);` - сделает трассировку стека вызовов
`s($var);` - выведет переменную в печатном виде
`sd($var);` - выведет переменную в печатном виде и остановит. Эквивалент `s();die;`

`Kint::enabled($_SERVER['REMOTE_ADDR'] === 'ваш-ip');` - поставьте перед вызовом, позволит видеть вывод только вашему айпишнику
Или раскомментируйте ее внутри файла `otshelnik-fm-kint.php` и впишите свой ip

**Я добавил тройку своих функций:**

`vd($var);` - (мой var_dump) - удобный дебаг вместо print_r или var_dump
`vdd($var);` - аналог vd, но с die; на конце. Когда нужно остановить дальнейшую работу
`vda($var);` - (var_dump admin) - вывод на экран для админа
`vdl($var);` - (var_dump log) - пишем в логи сервера. Когда выводить на экран нам нельзя (или это дебаг ajax запроса например).


в `otshelnik-fm-kint.php` можно выбрать шаблон темы оформления для вывода данных дебага через Kint. Строка `Kint::$theme = 'original';`

-----------

## Changelog

**2017-03-15**

v1.0.0
* Release

-----------

## Author

**Wladimir Druzhaev** (Otshelnik-Fm)

-----------

## License

Licensed under the MIT License
