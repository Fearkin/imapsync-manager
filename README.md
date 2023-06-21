
```
 _                                                                                               
(_)                                                                                              
 _ _ __ ___   __ _ _ __  ___ _   _ _ __   ___ ______ _ __ ___   __ _ _ __   __ _  __ _  ___ _ __ 
| | '_ ` _ \ / _` | '_ \/ __| | | | '_ \ / __|______| '_ ` _ \ / _` | '_ \ / _` |/ _` |/ _ \ '__|
| | | | | | | (_| | |_) \__ \ |_| | | | | (__       | | | | | | (_| | | | | (_| | (_| |  __/ |   
|_|_| |_| |_|\__,_| .__/|___/\__, |_| |_|\___|      |_| |_| |_|\__,_|_| |_|\__,_|\__, |\___|_|   
                  | |         __/ |                                               __/ |          
                  |_|        |___/                                               |___/                                                                       
```

# ОПИСАНИЕ

imapsync-manager - скрипт на bash надстройка над утилитой imapsync, скрипт помогает мигрировать и проверить размер почты, также определяет почтовые ящики с которыми есть проблемы доступа, скрипт примечателен тем что выводит аккуратную и понятную информацию, в человеко читаемом виде.

# УСТАНОВКА

!ВНИМАНИЕ - *сама утилита уже должны быть установлена в системе проверьте просто запустив в консоли imapsync
если утилита отсутствует установите следуя руководству автора*  https://imapsync.lamiral.info/#install

```
git clone https://github.com/solo10010/imapsync-manager
cd imapsync-manager
chmod +x sync.sh
./sync.sh --help
```

Для использования утилиты на почтовых ящиках создайте файл listmail.txt

```
touch listmail.txt
```

Заполните файл следую этому шаблону

```
хост001_1;пользователь001_1;пароль001_1;хост001_2;пользователь001_2;пароль001_2;
хост002_1;пользователь002_1;пароль002_1;хост002_2;пользователь002_2;пароль002_2;
хост003_1;пользователь003_1;пароль003_1;хост003_2;пользователь003_2;пароль003_2;
```

# СПРАВКА

```
~/imapsync-manager (master*) # ./sync.sh --help                               

 Использование: ./sync.sh [options...] -f --file <email_sunc.txt>
                -m --migrate <start_mail_migrate> -s --size <check_mail_size>

  -f, --file            <mail.txt> Выбор файла с внесенными ящиками для переноса
  -m, --migrate         Запустить миграцию почты из файла выбранного в -f
  -s, --size            проверить размер почты на переносимых и перенесенных ящиках из файла -f

  Пример заполнения почтовых ящиков в файл для переноса

  хост001_1;пользователь001_1;пароль001_1;хост001_2;пользователь001_2;пароль001_2;
  хост002_1;пользователь002_1;пароль002_1;хост002_2;пользователь002_2;пароль002_2;
  хост003_1;пользователь003_1;пароль003_1;хост003_2;пользователь003_2;пароль003_2;

```

# ПРИМЕРЫ ЗАПУСКА

Проверить ращзмер почтовых ящиков
```
./sync.sh --file listmail.txt --size
```

Запустить миграци всех почтовых ящиков

```
./sync.sh --file listmail.txt --migrate
```

Примеры вывода утилиты в разных режимах запуска

```
~/imapsync-manager (master*) # ./sync.sh --file listmail.txt --size                               
==================== start check mails (3)  =====================
perenos1@oibai.ru: success login MailSize:5.14 MB Folder:5 -> perenos2@oibai.ru: success login MailSize:5.14 MB Folder:5 <-> SUCCES!
perenos3@oibai.ru: success login MailSize:0 KB Folder:5 -> perenos4@oibai.ru: success login MailSize:0 KB Folder:5 <-> SUCCES!
perenos3@oibai.ru: failed login MailSize:0 KB Folder: -> perenos4@oibai.ru: failed login MailSize:0 KB Folder: <X> FAILED!

====================== SOURCE MAIL ==============================
SOURCE      Total Mail Size: 5.14 MB
SOURCE      Total Folder Count: 10
=================== DESTANATION MAIL ============================
DESTENATION Total Mail Size:  5.14 MB
DESTENATION Total Folder Count: 10

============ Error Summary sync_errors.log ======================
NO ERROR LOG FILE

```

```
~/imapsync-manager (master*) # ./sync.sh --file listmail.txt --migrate
================== start migrate mails (3)  =====================
perenos1@oibai.ru: success login -> perenos1@oibai.ru: success login -> SUCCES!
perenos3@oibai.ru: success login -> perenos3@oibai.ru: success login -> SUCCES!
perenos3@oibai.ru: failed login -> perenos3@oibai.ru: failed login -X FAILED!

============ Error Summary sync_errors.log ======================
NO ERROR LOG FILE
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
~/imapsync-manager (master*) #                                 
```


