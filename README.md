

# Домашнее задание к занятию 13.3 «Уязвимости и атаки на информационные системы» - Соловьёв Андрей SYS-18

---

## Задание 1

Скачайте и установите виртуальную машину Metasploitable: https://sourceforge.net/projects/metasploitable/.

![installed.PNG](https://github.com/Andrewsolo1969/13-1-hw/blob/main/img/installed.PNG)

IP address 192.168.55.79

Это типовая ОС для экспериментов в области информационной безопасности, с которой следует начать при анализе уязвимостей.

Просканируйте эту виртуальную машину, используя nmap.

Попробуйте найти уязвимости, которым подвержена эта виртуальная машина.

Сами уязвимости можно поискать на сайте https://www.exploit-db.com/.

Для этого нужно в поиске ввести название сетевой службы, обнаруженной на атакуемой машине, и выбрать подходящие по версии уязвимости.

Ответьте на следующие вопросы:

Какие сетевые службы в ней разрешены?

![sevices.PNG](https://github.com/Andrewsolo1969/13-1-hw/blob/main/img/sevices.PNG)

Какие уязвимости были вами обнаружены? (список со ссылками: достаточно трёх уязвимостей)

21/tcp   open  ftp         vsftpd 2.3.4
vsftpd 2.3.4 - Backdoor Command Execution (Metasploit) - https://www.exploit-db.com/exploits/17491

5432/tcp open  postgresql  PostgreSQL DB 8.3.0 - 8.3.7
PostgreSQL 8.2/8.3/8.4 - UDF for Command Execution - https://www.exploit-db.com/exploits/7855

2121/tcp open  ftp         ProFTPD 1.3.1 - ProFTPd IAC 1.3.x - Remote Command Execution
https://www.exploit-db.com/exploits/15449



Или с использованием скрипта Vulners. nse –  скрипт расширяющий возможности NMAP и позволяющий использовать результаты сканирования для поиска уязвимостей сетевых устройств и сервисов в большой базе данных vulners.com:

ссылки https://vulners.com/ либо https://www.exploit-db.com/ - на скринах


![vulners1.PNG](https://github.com/Andrewsolo1969/13-1-hw/blob/main/img/vulners1.PNG)

![vulners2.PNG](https://github.com/Andrewsolo1969/13-1-hw/blob/main/img/vulners2.PNG)

![vulners3.PNG](https://github.com/Andrewsolo1969/13-1-hw/blob/main/img/vulners3.PNG)

![vulners4.PNG](https://github.com/Andrewsolo1969/13-1-hw/blob/main/img/vulners4.PNG)


## Задание 2

Проведите сканирование Metasploitable в режимах SYN, FIN, Xmas, UDP. Запишите сеансы сканирования в Wireshark.
Ответьте на следующие вопросы:
Чем отличаются эти режимы сканирования с точки зрения сетевого трафика? Как отвечает сервер? Приведите ответ в свободной форме.


Судя по  wireshark трафик отличается флагами в случае сканирования TCP портов, так SYN сканирование не до конца устанавливает соединение, т.к. флаг FIN отсутсвует в таком трафике.

Из мануала https://nmap.org/man/ru/man-port-scanning-techniques.html

-sS (TCP SYN сканирование) - SYN это используемый по умолчанию и наиболее популярный тип сканирования. 
Эту технику часто называют сканированием с использованием полуотрытых соединений, т.к. вы не открываете полного TCP соединения. Вы посылаете SYN пакет, как если бы вы хотели установить реальное соединение и ждете. Ответы SYN/ACK указывают на то, что порт прослушивается (открыт), а RST (сброс) на то, что не прослушивается.

![SYN.PNG](https://github.com/Andrewsolo1969/13-1-hw/blob/main/img/SYN.PNG)


Трафик при UDP сканировании выгляит совсем иначе, так в случае закрытого порта, в ответ приходит ICMP ошибка.

Не во всех режимах сканирования гарантировано определяется открыт порт или фильтруется, только в случае SYN это можно определить точно. Опять же при сканировании UDP определяются только UDP порты.

Из мануала https://nmap.org/man/ru/man-port-scanning-techniques.html

-sU (Различные типы UDP сканирования):

UDP сканирование работает путем посылки пустого (без данных) UDP заголовка на каждый целевой порт. Если в ответ приходит ICMP ошибка о недостижимости порта (тип 3, код 3), значит порт закрыт. 

![udp.PNG](https://github.com/Andrewsolo1969/13-1-hw/blob/main/img/udp.PNG)



















 
