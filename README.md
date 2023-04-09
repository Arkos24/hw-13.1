# Домашнее задание к занятию "`Уязвимости и атаки на информационные системы`" - `Мельников Семен`




### Задание 1

Список разрешенных служб:

21/tcp   open  ftp
22/tcp   open  ssh
23/tcp   open  telnet
25/tcp   open  smtp
53/tcp   open  domain
80/tcp   open  http
111/tcp  open  rpcbind
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
512/tcp  open  exec
513/tcp  open  login
514/tcp  open  shell
1524/tcp open  ingreslock
2049/tcp open  nfs
2121/tcp open  ccproxy-ftp
3306/tcp open  mysql
3632/tcp open  distccd
5432/tcp open  postgres
5900/tcp open  vnc
6000/tcp open  X11
6667/tcp open  irc
8009/tcp open  ajp13

Обнаруженные уязвимости:
1)по порту tcp/21 (FTP):
vsftpd 2.3.4 - Backdoor Command Execution (Metasploit)
https://www.exploit-db.com/exploits/17491

2)по порту tcp/139:
Samba 3.5.0 - Remote Code Execution
https://www.exploit-db.com/exploits/42060

3) порты 21 и 80 (необязательно) демон ProFTPd
ProFTPd 1.3.5 - 'mod_copy' Remote Command Execution (2)
https://www.exploit-db.com/exploits/49908


---

### Задание 2

SYN-сканирование не завершает установку соединения TCP, суть его работы - на запрос прилетает ответ либо syn-ack (порт открыт), либо rst (порт закрыт), работает быстро
FIN-сканирование в отличии от SYN либо получает ответ RST,обозначающий закрытый порт, либо никакого ответа - то есть порт открыт, работает медленно из-за вынужденного ожиданя ответа
Xmas-сканирование шлет TCP-пакеты с флагами FIN,URG,PSH, в отвт ожидавние либо RST(закрыт порт), либо ничего - то есть порт открыт, из-за времени ожидания ответа также медленнее
UPD-сканирование не устанавливает никаких соединений, отправляются пустые датаграммы, в ответ прилетает либо ICMP-ответ о недоступности порта, либо ничего, что значит открытость нужного порта. Метод ненадежный из-за особенности UDP-доставка не гарантирована,поэтмоу отсутствие ответа может быть не признаком открытости порта,а что датаграмма не дошла до цели, наверняка узнать нельзя, в идеале сканирование проводить несколько раз или пользоваться другими методами
