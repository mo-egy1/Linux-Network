# Linux Network By Selysecr  شبكة لينكس

## Part 1. Tool **ipcalc**

- Обновим пакеты по необходимости:
  - `sudo apt-get update && sudo apt-get upgrade`
- Установим утилиту
  - `sudo apt-get -y install ipcalc`


### 1.1. Sets and masks - Сети и маски

* 1) Определили адрес сети с помощью команды 
 `ipcalc 192.167.38.54/13 | grep Network`
 


  ![Part_1](/src/images/part1/1_1_1.png)

 * 2) Перевод маски 255.255.255.0 в префиксную и двоичную запись 
 `ipcalc 192.167.38.54/255.255.255.0`
 
![Part_1](/src/images/part1/1_1_2_1.png) 

 *  Перевод /15 в обычную и двоичную
 
![Part_1](/src/images/part1/1_1_2_2.png) 

 * Перевод 11111111.11111111.11111111.11110000 в обычную и префиксную
 
![Part_1](/src/images/part1/1_1_2_3.png) 

![Part_1](/src/images/part1/1_1_2_3_1.png)

 
  * 3) Минимальный и максимальный хост в сети 12.167.38.4 при маске /8 - Макс. хост 12.255.255.254, Мин. хост 12.0.0.1


![Part_1](/src/images/part1/1_1_3_1.png) 

 * Минимальный и максимальный хост при маске 11111111.11111111.00000000.00000000 - Макс. хост 12.167.255.254, Мин. хост 12.167.0.1

 ![Part_1](/src/images/part1/1_1_3_2.png) 
 
 ![Part_1](/src/images/part1/1_1_3_2_1.png) 

 * Минимальный и максимальный хост при маске 255.255.254.0 - Макс. хост 12.167.39.254, Мин. хост 12.167.38.1



 ![Part_1](/src/images/part1/1_1_3_3.png) 
  
 * Минимальный и максимальный хост при маске /4 - Макс. хост 15.255.255.254, Мин. хост 0.0.0.1


  ![Part_1](/src/images/part1/1_1_3_4.png) 


###  1.2. localhost

* IP 194.34.23.100 --> No

  ![Part_1](/src/images/part1/1_2_1.png)
  
* IP 127.0.0.2 --> Yes 

  ![Part_1](/src/images/part1/1_2_2.png)

* IP 127.1.0.1 --> Yes
 
  ![Part_1](/src/images/part1/1_2_3.png)
  
* IP 128.0.0.1 --> No

  ![Part_1](/src/images/part1/1_2_4.png)

 ### 1.3. Network ranges and segments
 
* 1) which can be public and which private
 
* 10.0.0.45 - private
 
   ![Part_1](/src/images/part1/1_3_1.png)
   
* 134.43.0.2 - public

   ![Part_1](/src/images/part1/1_3_2.png)

* 192.168.4.2 - private

   ![Part_1](/src/images/part1/1_3_3.png)
   
* 172.20.250.4 - private

   ![Part_1](/src/images/part1/1_3_4.png)
   
* 172.0.2.1 - public 

   ![Part_1](/src/images/part1/1_3_5.png)
   
   
* 192.172.0.1 - public


   ![Part_1](/src/images/part1/1_3_6.png)
   
* 172.68.0.2 - public

   ![Part_1](/src/images/part1/1_3_7.png)

* 172.16.255.255 - private

   ![Part_1](/src/images/part1/1_3_8.png)
   
* 10.10.10.10 - private

   ![Part_1](/src/images/part1/1_3_9.png)
   
* 192.169.168.1 - public 

   ![Part_1](/src/images/part1/1_3_10.png)
   
   
* 2) Which of the listed gateway IP addresses are possible on the 10.10.0.0/18 network:10.0.0.1 (not possible), 10.10.0.2 (possible), 10.10.10.10 (possible), 10.10.100.1 (not possible), 10.10. 1.255( possible)



## Part 2. Static routing between two machines
* Подняли 2 вирутальные машины ws1 и ws2 в virtualBox
    
 ![Part_1](/src/images/part2/1.png)

* С помощью команды ip a посмотрели существующие сетевые интерфейсы.

   ![Part_2](/src/images/part2/2.png)


* Задали следующие адреса и маски: ws1 - 192.168.100.10, маска /16, ws2 - 172.24.116.8, маска /12

   ![Part_2](/src/images/part2/3.png)
  

* Выполнили команду netplan apply для перезапуска сервиса. Выводим таблицу маршрутизации.

   ![Part_2](/src/images/part2/4.png)
   ![Part_2](/src/images/part2/5.png)
  
  
### 2.1. Adding a static route manually

* Добавили статический маршрут от одной машины до другой и обратно при помощи команды вида `ip r add <ip> dev enp0s3`

   ![Part_2](/src/images/part2/2_1.png) 
  
  
* Пропинговать соединение между машинами

   ![Part_2](/src/images/part2/2_2.png) 

### 2.2. Adding a static route with saving

* Добавили статический маршрут от одной машины до другой с помощью файла etc/netplan/00-installer-config.yaml

   ![Part_2](/src/images/part2/2_3.png) 

* Пропинговали соединение между машинами

   ![Part_2](/src/images/part2/2_4.png) 


## Part 3. iperf3 utility
### 3.1. Connection speed

* Базовой единицей скорости передачи информации является бит в секунду (бит/с). Разница между байтами в секунду (Б/с) и битами в секунду (бит/c) такая же, как разница между байтами (Б) и битами (бит): 1 Б/с = 8 бит/с. Точно так же разница между килобайтами в секунду (КБ/с) и Б/с такая же, как разница между килобайтами и байтами: 1 КБ/с = 1024 Б/с. И так далее.


### Перевести и записать в отчёт:

 * 8 Mbps (мегабит в секуду) = 1 MB/s (мегабайт в секунду)

 * 100 MB/s (мегабайт в секунду) = 800 000 Kbps (килобит в секунду)

 * 1 Gbps (гигабит в секунду) = 1 000 Mbps (мегабит в секунду)



### 3.2. iperf3 utility

* Измерили скорость соединения между ws1 и ws2. Перед этии установили утилиту ipref3 командой `sudo apt-get install iperf3` 


   ![Part_3](/src/images/part3/1.png)
  
  
   ![Part_3](/src/images/part3/2.png)
   
   
   ![Part_3](/src/images/part3/2.png)



## Part 4. Network firewall

### 4.1. iptables utility

* iptables — это утилита брандмауэра командной строки, которая использует цепочки политик для разрешения или блокировки трафика. Когда соединение пытается установиться в системе, iptables ищет правило в своем списке, чтобы сопоставить его. Если утилита не находит нужного правила, она прибегает к действию по умолчанию.

* Подсистема iptables и Netfilter уже достаточно давно встроена в ядро Linux. Все сетевые пакеты, которые проходят через компьютер, отправляются компьютером или предназначены компьютеру, ядро направляет через фильтр iptables. Там эти пакеты поддаются проверкам и затем для каждой проверки, если она пройдена выполняется указанное в ней действие. Например, пакет передается дальше ядру для отправки целевой программе, или отбрасывается.


* Переходим в кореневой каталог

  - `cd`

* Создаем файл `/etc/firewall.sh`, имитирующий фаерволл, на `ws1` и `ws2` с помощью команды

 - `sudo touch /etc/firewall.sh`
 
 
   ![Part_4](/src/images/part4/1.png)
   
   
   
* Добавляем в файл следующие правила согласно задания:   


- `sudo nano /etc/firewall.sh`

* 1. на `ws1` применить стратегию когда в начале пишется запрещающее правило, а в конце пишется разрешающее правило (это касается пунктов 4 и 5).

* 2. на `ws2` применить стратегию когда в начале пишется разрешающее правило, а в конце пишется запрещающее правило (это касается пунктов 4 и 5).

* 3. открыть на машинах доступ для порта 22 (ssh) и порта 80 (http).

* 4. запретить echo reply (машина не должна "пинговаться”, т.е. должна быть блокировка на OUTPUT).

* 5. разрешить echo reply (машина должна "пинговаться").



   ![Part_4](/src/images/part4/2.png)
   

* Запустим файлы на обеих машинах командами


- `sudo chmod +x /etc/firewall.sh`

- `sudo chmod +x /etc/firewall.sh`

   ![Part_4](/src/images/part4/3.png)

* Разница между стратегиями, применёнными в первом и втором файлах, заключается в следующем: в утилите `iptables` правила выполняются сверху вниз. На первой машине первым указано запрещающее правило на выход, поэтому она не сможет пропинговать другую машину. У второй машины, наоброт - первым указано разрешающее правило, значит она сможет пропинговать другую машину.



### 4.2. nmap utility

* nmap - это очень популярный сканер сети, для исследования сети и аудита безопасности. Он имеет открытый исходный код, который может использоваться как в Windows, так и в Linux.

* Эта программа помогает системным администраторам очень быстро понять какие компьютеры подключены к сети, узнать их имена, а также посмотреть какое программное обеспечение на них установлено, какая операционная система и какие типы фильтров применяются.

* Этот инструмент обычно используется хакерами и энтузиастами кибербезопасности, а также сетевыми и системными администраторами. Он используется для следующих целей:

  * информация о сети в режиме реального времени;
  * подробная информация обо всех IP-адресах, активированных в вашей сети;
  * количество открытых портов в сети;
  * предоставить список живых хостов;
  * сканирование портов, ОС и хостов;
  * посмотреть типы применямых фильтров. Например, с помощью скриптов можно автоматически обнаруживать новые уязвимости безопасности в сети. Чаще всего nmap используется для сканирования системы по имени хоста или IP-адресу. Одной из особенностей nmap является то, что эта утилита может определить, включен ли хост, даже если его нельзя пропинговать.


4.2.1 Поиск машины, которая не "пингуется"

- `ping IP-address` 


   ![Part_4](/src/images/part4/2_1.png)


 
 - `sudo nmap IP-address`
 
 * Запускаем утилиту `nmap` командой (для проверки ищем в выводе nmap наличие строки Host is up)

- `sudo nmap IP-address`

   ![Part_4](/src/images/part4/2_2.png)




### 4.2.2 Сохраняем дампы образов виртуальных машин.

* Для сохранения образов машины в настройках машины выбираем Опции - Снимки.



   ![Part_4](/src/images/part4/2_3.png)
   
   
   
   
## Part 5. Static network routing

* We need to make this Network routing


   ![Part_5](/src/images/part5/5_1.png)
   
### 5.1. Configuration of machine addresses

* Set up the machine configurations in etc/netplan/00-installer-config.yaml according to the network in the picture.

* etc/netplan/00-installer-config.yaml

### ws11:

   ![Part_5](/src/images/part5/5_1_2.png)


### ws21:


   ![Part_5](/src/images/part5/5_1_3.png)


### ws22:

   ![Part_5](/src/images/part5/5_1_4.png)
   
   
### r1:

   ![Part_5](/src/images/part5/5_1_5.png)


### r2: 

   ![Part_5](/src/images/part5/5_1_6.png)
   
   
   
### Check that the machine address is correct with the ip -4


* ws11:

   ![Part_5](/src/images/part5/5_1_7.png)


* ws21: 

   ![Part_5](/src/images/part5/5_1_8.png)
   
* ws22 

   ![Part_5](/src/images/part5/5_1_9.png)
   
* r1:

   ![Part_5](/src/images/part5/5_1_10.png)

* r2:

   ![Part_5](/src/images/part5/5_1_11.png)



### 5.2. Enabling IP forwarding.

* To enable IP forwarding, run the following command on the routers: `sysctl -w net.ipv4.ip_forward=1`
* With this approach, the forwarding will not work after the system is rebooted.

* Add a screenshot with the call and output of the used command to the report


* r1:

   ![Part_5](/src/images/part5/5_2_1.png)


* r2:

   ![Part_5](/src/images/part5/5_2_2.png)
   
   
### Open /etc/sysctl.conf file and add the following line:

    `net.ipv4.ip_forward = 1`
    
    
* r1: 

   ![Part_5](/src/images/part5/5_2_3.png)
   
*r2:

   ![Part_5](/src/images/part5/5_2_4.png)   
   
   
### 5.3. Default route configuration


* Configure the default route (gateway) for the workstations. To do this, add default before the router's IP in the configuration file


* Add a screenshot of the etc/netplan/00-installer-config.yaml file to the report.


* ws11: 

   ![Part_5](/src/images/part5/5_3_1.png)


* ws21 

   ![Part_5](/src/images/part5/5_3_2.png)


* ws22

   ![Part_5](/src/images/part5/5_3_3.png)


### Call ip r and show that a route is added to the routing table

* ws11:

   ![Part_5](/src/images/part5/5_3_4.png)
   
   
* ws21:

   ![Part_5](/src/images/part5/5_3_5.png)

* ws22: 

   ![Part_5](/src/images/part5/5_3_6.png)

### Ping r2 router from ws11 and show on r2 that the ping is reaching. To do this, use the `tcpdump -tn -i eth1`


* ws11:

   ![Part_5](/src/images/part5/5_3_7.png)


* r2: 

   ![Part_5](/src/images/part5/5_3_8.png)



### 5.4. Adding static routes

* Add static routes to r1 and r2 in configuration file. Here is an example for r1 route to 10.20.0.0/26


` # Add description to the end of the eth1 network interface: `
`- to: 10.20.0.0`
 ` via: 10.100.0.12 `



* r1: 

   ![Part_5](/src/images/part5/5_4_1.png)


* r2:

   ![Part_5](/src/images/part5/5_4_2.png)


### Call `ip r` and show route tables on both routers. Here is an example of the r1 table:


* r1:

   ![Part_5](/src/images/part5/5_4_3.png)

* r2:

   ![Part_5](/src/images/part5/5_4_4.png)
   
   
### Run `ip r list 10.10.0.0/[netmask]` and `ip r list 0.0.0.0/0` commands on ws11.


   ![Part_5](/src/images/part5/5_4_5.png)


### Explain

``` The default route has a lower priority and is triggered when no suitable route is found in the routing table. 0.0.0.0/0 is a non-routable address that can be used for a variety of purposes, mainly as a default address or a placeholder address. The default route has a lower priority and is triggered when no suitable route is found in the routing table. We created a rule for network 10.10.0.0, and the created route is used accordingly. You can also set a metric to change route priorities. ```




### 5.5. Making a router list 

 Для установки утилиты на `ws11` используем команду
 
 - `sudo apt install traceroute`

* Run the `tcpdump -tnv -i eth0` dump command on r1


   ![Part_5](/src/images/part5/5_5_1.png)


* The output of the used commands (tcpdump and traceroute) 


   ![Part_5](/src/images/part5/5_5_2.png)

### Explain 

``` First the data goes to the eth0 interface of the r1 router, then it gets routed to the second router using eth0 interface of r2 and finally gets routed to destination 10.20.0.10. ```



### 5.6. Using ICMP protocol in routing:


* Run on r1 network traffic capture going through eth0 with the
    `tcpdump -n -i eth0 icmp` command.

   ![Part_5](/src/images/part5/5_6_1.png)


* Ping a non-existent IP (e.g. 10.30.0.111) from ws11 with the
    `ping -c 1 10.30.0.111` command.

   ![Part_5](/src/images/part5/5_6_2.png)


* Сохранить дампы образов виртуальных машин p.s. Ни в коем случае не сохранять дампы в гит!



### Part 6. Dynamic IP configuration using DHCP

* First step it to install DHCP server:

    `apt install isc-dhcp-server`
    
* For r2, configure the DHCP service in the `/etc/dhcp/dhcpd.conf` file:


   ![Part_6](/src/images/part6/1.png)


### 2) write `nameserver 8.8.8.8.` in a resolv.conf file

   ![Part_6](/src/images/part6/2.png)


* Reboot the ws21 machine with `reboot` and show with `ip a` that it has got an address.


   ![Part_6](/src/images/part6/3.png)


* ping ws22 from ws21 


   ![Part_6](/src/images/part6/4.png)
   
   
* Specify MAC address at ws11 by adding to etc/netplan/00-installer-config.yaml:

`macaddress: 10:10:10:10:10:BA`, `dhcp4: true`


   ![Part_6](/src/images/part6/5.png)



* Сonfigure `r1` the same way as `r2`, but make the assignment of addresses strictly linked to the MAC-address `(ws11)`.



   ![Part_6](/src/images/part6/6.png)

* Run the same tests` ip a`:

   ![Part_6](/src/images/part6/7.png)


* Also ping `r1` from `ws1`:

   ![Part_6](/src/images/part6/8.png)


### Request ip address update from ws21


   ![Part_6](/src/images/part6/9.png)

* Describe in the report what DHCP server options were used in this point.

* `Option routers [10.0.0.0,...]` the routers option specifies a list of IP addresses for routers on the client's subnet. Routers should be listed in order of preference

* `Option domain-name-servers [10.0.0.0, ...]` domain-name-servers option specifies a list of Domain Name System (STD 13, RFC 1035) name servers available to the client. Servers should be listed in order of preference.


* Сохранить дампы образов виртуальных машин p.s. Ни в коем случае не сохранять дампы в гит!


### Part 7. NAT

 * To work with the apache2 server, install it on machines r1, r2 and ws22. Perhaps apache2 will not install, then maybe updating the system will help (see below).
 
 - `sudo apt install apache2`


* Обновление системы(Updata)

- ` sudo apt update`

- ` sudo apt upgrade `

### 7.1 

* In /etc/apache2/ports.conf file change the `line Listen 80` to `Listen 0.0.0.0:80`on ws22 and r1, i.e. make the Apache2 server public


* r1:

   ![Part_7](/src/images/part7/1.png)

* ws22: 

   ![Part_7](/src/images/part7/2.png)



* Start the Apache web server with `service apache2 start` command on ws22 and r1

   ![Part_7](/src/images/part7/3.png)



### Add the following rules to the firewall, created similarly to the firewall from Part 4, on r2:

1) delete rules in the filter table - `iptables -F`

2) delete rules in the "NAT" table - `iptables -F -t nat`

3) drop all routed packets - `iptables --policy FORWARD DROP`


   ![Part_7](/src/images/part7/4.png)


* Run the File as in Part4 

   ![Part_7](/src/images/part7/5.png)


* Check the connection between ws22 and r1 with the ping command

   ![Part_7](/src/images/part7/6.png)



* 4) allow routing of all ICMP protocol packets

- ` sudo nano /etc/apache2/ports.conf `


   ![Part_7](/src/images/part7/7.png)
   

- ` sudo bash /etc/firewall.sh `   
   
   ![Part_7](/src/images/part7/8.png)


* Check connection between `ws22` and `r1` with the `ping`command

- `ping -c 5 10.100.0.11`


   ![Part_7](/src/images/part7/9.png)


* Add two more rules to the file:

* 5) enable SNAT, which is masquerade all `local ip` from the local network behind `r2` (as defined in Part 5 - `network 10.20.0.0`)

* Tip: it is worth thinking about routing internal packets as well as external packets with an established connection


### 6) enable DNAT on `port 8080` of `r2` machine and add external network access to the Apache web server running on `ws22`


* Tip: be aware that when you will try to connect, there will be a new tcp connection for `ws22` and `port 80`



   ![Part_7](/src/images/part7/10.png)


* Run the file as in Part 4

- ` etc/firewall.sh`


   ![Part_7](/src/images/part7/11.png)

* Before testing it is recommended to disable the NAT network interface in VirtualBox (its presence can be checked with ip a command), if it is enabled


* Check the TCP connection for SNAT by connecting from ws22 to the Apache server on r1 with the` telnet 10.10.0.1 80` command

   ![Part_7](/src/images/part7/12.png)



* Check the TCP connection for DNAT by connecting from r1 to the Apache server on ws22 with the `telnet 10.100.0.12 808`


   ![Part_7](/src/images/part7/13.png)


* Save dumps of virtual machine images



### Part 8. Bonus. Introduction to SSH Tunnels


* Run a firewall on `r2` with the rules from Part 7


   ![Part_8](/src/images/part8/1.png)


- `sudo vim /etc/firewall.sh`

- `sudo /etc/firewall.sh`


### Start the Apapche web server on ws22 on localhost only (i.e. in /etc/apache2/ports.conf file change the line `Listen 80` to Listen `localhost:80`)


   ![Part_8](/src/images/part8/2.png)



- `sudo vim /etc/apache2/ports.conf`

- `sudo service apache2 start`


   ![Part_8](/src/images/part8/3.png)




* Use Local TCP forwarding from `ws21` to `ws22` to access the web server on `ws22` from `ws21`


- `ssh -L 7777:localhost:80 10.20.0.20`


   ![Part_8](/src/images/part8/4.png)


* Use Remote TCP forwarding from `ws11` to `ws22` to access the web server on `ws22` from `ws11`

- `ssh -R 7777:localhost:80 10.20.0.20`

   ![Part_8](/src/images/part8/5.png)


* To check if the connection worked in both of the previous steps, go to a second terminal (e.g. with the Alt + F2) and run the `telnet 127.0.0.1 [local port]` command.



   ![Part_8](/src/images/part8/6.png)


### Save dumps of virtual machine images

- `p.s. Do not upload dumps to git under any circumstances!`
