###########################
Модуль двигательной активности
###########################

.. image:: images/module_bno055.jpg

==========================
Технические характеристики
==========================

* Размеры: TBA

* Напряжение питания: TBA

* Потребляемые ток, пиковый: TBA

==========================
Подключение к головному устройству
==========================

Подключение к головному устройству осуществляется по протоколу RS-485 через разъем SH04, расположенному на плате. Распиновка приведена на рисунке ниже.

.. image:: images/sh04w.png

==========================
Выполняемые команды
==========================

**************************
Команда на получение углов Эйлера
**************************

Формат запроса
==========================

Длина запроса - **8** байт.

+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| Байт # | Поле        | Тип            | Значение      | Описание                                                       |
+========+=============+================+===============+================================================================+
| 0      | start_byte  | uint8_t        | **0xAA**      | Стартовый байт.                                                |
|        |             |                |               | Всегда равен **0xAA**                                          |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 1      | id          | uint8_t        | **0x30**      | Идентификатор получателя пакета.                               |
|        |             |                |               | **0x30** - получатель - *Датчик ДА*                            |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 2      | type        | uint8_t        | **0x01**      | Тип пакета.                                                    |
|        |             |                |               | **0x01** - пакет команды управления                            |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 3      | action      | uint8_t        | **0x00**      | *Действие*, которое необходимо выполнить.                      |
|        |             |                |               | **0x00** - *Чтение*                                            |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 4      | param       | uint8_t        | **0x30**      | Параметр для *действия*.                                       |
|        |             |                |               | **0x30** - *Данные углов Эйлера*.                              |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 5      | data        | uint8_t        | **0x00**      | Данные для *действия*.                                         |
|        |             |                |               | **0x00** - нет данных                                          |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 6      | payload     | uint8_t        | **0x00**      | Дополнительные данные для *действия*.                          |
|        |             |                |               | **0x00** - нет данных                                          |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 7      | checksum    | uint8_t        | **0x0B**      | Котрольная сумма пакета - младший                              |
|        |             |                |               | байт суммы всех байтов пакета                                  |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+

Формат ответа
==========================

Длина ответа - **20** байт.

+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| Байт # | Поле        | Тип            | Значение      | Описание                                                       |
+========+=============+================+===============+================================================================+
| 0      | start_byte  | uint8_t        | **0xAA**      | Стартовый байт. Всегда равен **0xAA**                          |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 1      | id          | uint8_t        | **0x01**      | Идентификатор получателя пакета                                |
|        |             |                |               | **0x01** - получатель - *Головной модуль*                      |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 2      | type        | uint8_t        | **0x30**      | **0x30** - *Данные углов Эйлера*                               |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 3      | systime     | uint32_t       | 0xXX          | Системное время модуля в миллисекундах.                        |
+--------+             +                +---------------+                                                                +
| 4      |             |                | 0xXX          | Порядок байт - **little endian**                               |
+--------+             +                +---------------+                                                                +
| 5      |             |                | 0xXX          |                                                                |
+--------+             +                +---------------+                                                                +
| 6      |             |                | 0xXX          |                                                                |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 7      | heading     | uint16_t       | 0xXX          | Один из углов Эйлера - рысканье. 1 градус = 16 LSB             |
+--------+             +                +---------------+                                                                +
| 8      |             |                | 0xXX          | Порядок байт - **little endian**                               |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 9      | roll        | uint16_t       | 0xXX          | Один из углов Эйлера - крен. 1 градус = 16 LSB                 |
+--------+             +                +---------------+                                                                +
| 10     |             |                | 0xXX          | Порядок байт - **little endian**                               |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 11     | pitch       | uint16_t       | 0xXX          | Один из углов Эйлера - тангаж. 1 градус = 16 LSB               |
+--------+             +                +               +                                                                +
| 12     |             |                |               | Порядок байт - **little endian**                               |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 13     | lin_acc_x   | uint16_t       | 0xXX          | Линейное ускорение по оси X. 1 м/с^2 = 100 LSB                 |
+--------+             +                +               +                                                                +
| 14     |             |                |               | Порядок байт - **little endian**                               |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 15     | lin_acc_y   | uint16_t       | 0xXX          | Линейное ускорение по оси Y. 1 м/с^2 = 100 LSB                 |
+--------+             +                +               +                                                                +
| 16     |             |                |               | Порядок байт - **little endian**                               |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 17     | lin_acc_z   | uint16_t       | 0xXX          | Линейное ускорение по оси Z. 1 м/с^2 = 100 LSB                 |
+--------+             +                +               +                                                                +
| 18     |             |                |               | Порядок байт - **little endian**                               |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 19     | checksum    | uint8_t        | 0xXX          | Контрольная сумма пакета - младший                             |
|        |             |                |               | байт суммы всех байтов пакета                                  |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+

Имплементация значений
==========================

* Поле **systime** содержит значение системного времени модуля с дискретностью миллисекунда

* Поле **heading** содержит значение одного из углов Эйлера - рысканье. Диапазон значений: от 0° до 360°. (поворот по часовой стрелке увеличивает значение)

* Поле **roll** содержит значение одного из углов Эйлера - крен. Диапазон значений: от -90° до 90°. (увеличивается с увеличинеим наклона) 

* Поле **pitch** содержит значение одного из углов Эйлера - тангаж. Диапазон значений: от -180° до 180° (поворот по часовой стрелке увеличивает значение)

* Поля **lin_acc_x**, **lin_acc_y**, **lin_acc_z** содержат значения линейного ускорения по соответствующим осям


Примеры
==========================

Все команды приведены в HEX-формате без указания **0x**

*Запрос:* ``AA 30 01 00 30 00 00 0B``

*Ответ:* ``AA 01 30 FA 27 00 00 00 00 C3 FE 98 FF 01 00 FE FF 00 00 52``

*Интерпретация ответа:* 

* тип пакета - данные кватерниона

* systime = 00 00 27 FA = 10 234 мc, 

* heading = 00 00 = 0°,

* roll = FE C3 = -19.8125°,

* pitch = FF 98 = -6.5°,

* acc_x = 00 01 = 0.01 м/с2,

* acc_y = FF FE = -0.02 м/с2,

* acc_z = 00 00 = 0 м/с2.


**************************
Команда на получение кватернионов
**************************

Формат запроса
==========================

Длина запроса - **8** байт.

+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| Байт # | Поле        | Тип            | Значение      | Описание                                                       |
+========+=============+================+===============+================================================================+
| 0      | start_byte  | uint8_t        | **0xAA**      | Стартовый байт.                                                |
|        |             |                |               | Всегда равен **0xAA**                                          |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 1      | id          | uint8_t        | **0x30**      | Идентификатор получателя пакета.                               |
|        |             |                |               | **0x30** - получатель - *Датчик ДА*                            |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 2      | type        | uint8_t        | **0x01**      | Тип пакета.                                                    |
|        |             |                |               | **0x01** - пакет команды управления                            |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 3      | action      | uint8_t        | **0x00**      | *Действие*, которое необходимо выполнить.                      |
|        |             |                |               | **0x00** - *Чтение*                                            |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 4      | param       | uint8_t        | **0x31**      | Параметр для *действия*.                                       |
|        |             |                |               | **0x40** - Данные кватернионов                                 |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 5      | data        | uint8_t        | **0x00**      | Данные для *действия*.                                         |
|        |             |                |               | **0x00** - нет данных                                          |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 6      | payload     | uint8_t        | **0x00**      | Дополнительные данные для *действия*.                          |
|        |             |                |               | **0x00** - нет данных                                          |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 7      | checksum    | uint8_t        | **0x0C**      | Контрольная сумма пакета - младший                             |
|        |             |                |               | байт суммы всех байтов пакета                                  |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+

Формат ответа
==========================

Длина ответа - **16** байт.

+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| Байт # | Поле        | Тип            | Значение      | Описание                                                       |
+========+=============+================+===============+================================================================+
| 0      | start_byte  | uint8_t        | **0xAA**      | Стартовый байт. Всегда равен **0xAA**                          |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 1      | id          | uint8_t        | **0x01**      | Идентификатор получателя пакета                                |
|        |             |                |               | **0x01** - получатель - *Головной модуль*                      |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 2      | type        | uint8_t        | **0x31**      | **0x31** - *Данные кватернионов*                               |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 3      | systime     | uint32_t       | 0xXX          | Системное время модуля в миллисекундах.                        |
+--------+             +                +---------------+                                                                +
| 4      |             |                | 0xXX          | Порядок байт - **little endian**                               |
+--------+             +                +---------------+                                                                +
| 5      |             |                | 0xXX          |                                                                |
+--------+             +                +---------------+                                                                +
| 6      |             |                | 0xXX          |                                                                |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 7      | w           | uint16_t       | 0xXX          | Значение кватерниона. 1 кватернион = 2^14 LSB                  |
+--------+             +                +---------------+                                                                +
| 8      |             |                | 0xXX          | Порядок байт - **little endian**                               |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 9      | x           | uint16_t       | 0xXX          | Значение кватерниона. 1 кватернион = 2^14 LSB                  |
+--------+             +                +---------------+                                                                +
| 10     |             |                | 0xXX          | Порядок байт - **little endian**                               |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 11     | y           |uint16_t        |0xXX           | Значение кватерниона. 1 кватернион = 2^14 LSB                  |
+--------+             +                +               +                                                                +
|12      |             |                |               | Порядок байт - **little endian**                               |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
|13      | z           |uint16_t        |0xXX           | Значение кватерниона. 1 кватернион = 2^14 LSB                  |
+--------+             +                +               +                                                                +
|14      |             |                |               | Порядок байт - **little endian**                               | 
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
|15      | checksum    | uint8_t        | 0xXX          | Контрольная сумма пакета - младший                             |
|        |             |                |               | байт суммы всех байтов пакета                                  |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+

Имплементация значений
==========================

* Поле **systime** содержит значение системного времени модуля с дискретностью миллисекунда

* Поля **w**, **x**, **y**, **z** содержат значения кватернионов


Примеры
==========================

Все команды приведены в HEX-формате без указания **0x**

*Запрос:* ``AA 30 01 00 31 00 00 0C``

*Ответ:* ``AA 01 31 A1 0E 00 00 F5 3E 8A 03 F4 0A FF FF 47``

*Интерпретация ответа:* 

* тип пакета - данные кватерниона

* systime = 00 00 0E A1 = 3745 мс, 

* w = 3E F5 = 0.98370361328125,

* x = 03 8A = 0.0552978515625,

* y = 0A F4 = 0.171142578125,

* z = FF FF = -0.00006103515625.


**************************
Команда на получение сырых данных
**************************

Формат запроса
==========================

Длина запроса - **8** байт.

+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| Байт # | Поле        | Тип            | Значение      | Описание                                                       |
+========+=============+================+===============+================================================================+
| 0      | start_byte  | uint8_t        | **0xAA**      | Стартовый байт.                                                |
|        |             |                |               | Всегда равен **0xAA**                                          |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 1      | id          | uint8_t        | **0x30**      | Идентификатор получателя пакета.                               |
|        |             |                |               | **0x30** - получатель - *Датчик ДА*                            |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 2      | type        | uint8_t        | **0x01**      | Тип пакета.                                                    |
|        |             |                |               | **0x01** - пакет команды управления                            |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 3      | action      | uint8_t        | **0x00**      | *Действие*, которое необходимо выполнить.                      |
|        |             |                |               | **0x00** - *Чтение*                                            |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 4      | param       | uint8_t        | **0x32**      | Параметр для *действия*.                                       |
|        |             |                |               | **0x32** - Сырые данные                                        |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 5      | data        | uint8_t        | **0x00**      | Данные для *действия*.                                         |
|        |             |                |               | **0x00** - нет данных                                          |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 6      | payload     | uint8_t        | **0x00**      | Дополнительные данные для *действия*.                          |
|        |             |                |               | **0x00** - нет данных                                          |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 7      | checksum    | uint8_t        | **0x0D**      | Контрольная сумма пакета - младший                             |
|        |             |                |               | байт суммы всех байтов пакета                                  |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+

Формат ответа
==========================

Длина ответа - **26** байт.

+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| Байт # | Поле        | Тип            | Значение      | Описание                                                       |
+========+=============+================+===============+================================================================+
| 0      | start_byte  | uint8_t        | **0xAA**      | Стартовый байт. Всегда равен **0xAA**                          |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 1      | id          | uint8_t        | **0x01**      | Идентификатор получателя пакета                                |
|        |             |                |               | **0x01** - получатель - *Головной модуль*                      |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 2      | type        | uint8_t        | **0x32**      | **0x32** - *Сырые данные*                                      |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 3      | systime     | uint32_t       | 0xXX          | Системное время модуля в миллисекундах.                        |
+--------+             +                +---------------+                                                                +
| 4      |             |                | 0xXX          | Порядок байт - **little endian**                               |
+--------+             +                +---------------+                                                                +
| 5      |             |                | 0xXX          |                                                                |
+--------+             +                +---------------+                                                                +
| 6      |             |                | 0xXX          |                                                                |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 7      | acc_x       | uint16_t       | 0xXX          | Данные акселерометра по оси X. 1 м/с^2 = 100 LSB               |
+--------+             +                +---------------+                                                                +
| 8      |             |                | 0xXX          | Порядок байт - **little endian**                               |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 9      | acc_y       | uint16_t       | 0xXX          | Данные акселерометра по оси Y. 1 м/с^2 = 100 LSB               |
+--------+             +                +---------------+                                                                +
| 10     |             |                | 0xXX          | Порядок байт - **little endian**                               |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 11     | acc_z       | uint16_t       | 0xXX          | Данные акселерометра по оси Z. 1 м/с^2 = 100 LSB               |
+--------+             +                +---------------+                                                                +
| 12     |             |                | 0xXX          | Порядок байт - **little endian**                               |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 13     | mag_x       | uint16_t       | 0xXX          | Данные магнитометра по оси X. 1 мкТ = 16 LSB                   |
+--------+             +                +---------------+                                                                +
| 14     |             |                | 0xXX          | Порядок байт - **little endian**                               |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 15     | mag_y       | uint16_t       | 0xXX          | Данные магнитометра по оси Y. 1 мкТ = 16 LSB                   |
+--------+             +                +---------------+                                                                +
| 16     |             |                | 0xXX          | Порядок байт - **little endian**                               |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 17     | mag_z       |                | 0xXX          | Данные магнитометра по оси Z. 1 мкТ = 16 LSB                   |
+--------+             +                +---------------+                                                                +
| 18     |             |                | 0xXX          | Порядок байт - **little endian**                               |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 19     | gyro_x      | int16_t        | 0xXX          | Данные гироскопа по оси X. 1 Dps = 16 LSB                      |
+--------+             +                +---------------+                                                                +
| 20     |             |                | 0xXX          | Порядок байт - **little endian**                               |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 21     | gyro_y      | int16_t        | 0xXX          | Данные гироскопа по оси Y. 1 Dps = 16 LSB                      |
+--------+             +                +---------------+                                                                +
| 22     |             |                | 0xXX          | Порядок байт - **little endian**                               |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 23     | gyro_z      | int16_t        | 0xXX          | Данные гироскопа по оси Z. 1 Dps = 16 LSB                      |
+--------+             +                +---------------+                                                                +
| 24     |             |                | 0xXX          | Порядок байт - **little endian**                               |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+
| 25     | checksum    | uint8_t        | 0xXX          | Контрольная сумма пакета - младший                             |
|        |             |                |               | байт суммы всех байтов пакета                                  |
+--------+-------------+----------------+---------------+----------------------------------------------------------------+

Имплементация значений
==========================

* Поле **systime** содержит значение системного времени модуля с дискретностью миллисекунда

* Поля **acc_x**, **acc_y**, **acc_z** содержат данные акселерометра по соответствующим осям

* Поля **mag_x**, **mag_y**, **mag_z** содержат данные магнитометра по соответствующим осям

* Поля **gyro_x**, **gyro_y**, **gyro_z** содержат данные гироскопа по соответствующим осям

Примеры
==========================

Все команды приведены в HEX-формате без указания **0x**

*Запрос:* ``AA 30 01 00 32 00 00 0D``

*Ответ:* ``AA 01 32 3F 0C 00 00 B7 FE 69 00 99 03 D0 00 C4 FF 77 FE FF FF 01 00 01 00 EA``

*Интерпретация ответа:* 

* тип пакета - сырые данные ДА

* systime = 00 00 0C 3F = 3135 мс, 

* acc_x = FE B7 = -3.29 м/с^2,

* acc_y =  00 69 = 1.05 м/с^2,

* acc_z = 03 99 = 9.21 м/с^2,

* mag_x = 00 D0 = 13 1 мкТ,

* mag_y = FF C4 = -3.75 1 мкТ,

* mag_z = FE 77 = -24.5625 1 мкТ,

* gyro_x = FF FF = -0.0625 Dps,

* gyro_y = 00 01 = 0.0625 Dps,

* gyro_z = 00 01 = 0.0625 Dps.

