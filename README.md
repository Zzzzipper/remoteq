### remoteq ###

1. Клиент-серверное приложение для получения данных и управления имитатором измерителя напряжения. 
2. Серверная часть сделана с использованием языка и стандартных библиотек языка c++. 
3. Клиентская часть - с ипользованием фреймворка Qt версии 5.12.3. 
4. Для соединения используется сокет типа ``AF_UNIX``;
5. Стандарт  С++ 17.
6. Протокол обмена реализован по варианту 2 из [задач](https://github.com/Zzzzipper/remoteq/blob/master/docs/%D0%97%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5%20%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B8%D1%81%D1%82%D1%83_23_04_20.pdf) на выполнение тестовой работы
7. Сборка и тестирование производилось в среде Kubuntu 20.04 LTS

##### Требования к программному обеспечению  для разработки #####

1. Установить cmake из пакетов дистрибутива. Для Ununtu:
   ``
   sudo apt-get install cmake
   ``
2. Если установлен версией старше Qt5.12.3, то лучше обновить уcтановку до нужной версии;
3. Если используется несколько дистрибутивов, то лучше выбрать выбрать необходимую с помощью ``qtchooser`` и переменной окружения ``QT_SELECT`` для работы с ``qmake`` из командной строки.

##### Сборка #####

1. После установки необходимого софта и клонирования проекта, нужно перейти в корневую лиректорию проекта и в командной строке запустить на выполнение сценарий
``
./build.sh
``
2. После этого, если ошибок не произойдет, исполняемые файлы ``remoteq`` (это сервер) и ``client`` должны обнаружиться в корневой директории ``bin``.
3. Оба проекта сконфигурированы для работы с ними в ``qtcreator`` - можно собирать и отлаживать. Для успешной работы среды разработки с проектом для ``cmake`` нужно правильно сконфигурировать настройки проекта в части последовательности выполнения ``make`` команд, удаления и прехода в нужную директорию. Для примера в репозиторий выложен файл ``CMakeLists.txt.user`` - можно скопировать нужный раздел из него;

##### Доработка #####
1. Для добавления новой команды необходимо сначала добавить ее индекс в перечисление ``uds_command_type`` в файле ``include/common.h`` в корне проекта;
2. Затем, добавить обработчик (лямбда функцию) в файле ``src/headmeters.cpp`` в методо ``operate`` - по шаблону тех, что уже там есть;
3. В клиенте добавить ``Q_INVOKABLE`` методы для передачи данных в Qml engine; 