<p>University: [ITMO University](https://itmo.ru/ru/)</p>
<p>Faculty: [FICT](https://fict.itmo.ru)</p>
<p>Course: [Introduction in routing](https://github.com/itmo-ict-faculty/introduction-in-routing)</p>
<p>Year: 2022/2023 </p>
<p>Group: K33202, K33212</p>
<p>Author: Guliaeva Alisa, Potitova Valentina </p>
<p>Lab: Lab1 </p>
<p>Date of create: 20.09.2022 </p>
<p>Date of finished: 18.11.2022</p>
<h1>Отчет по лабораторной №1</h1>
<h2>"Установка ContainerLab и развертывание тестовой сети связи"</h2>
<ul>
<li>Файл, который использовали для развертывания тестовой сети, находится в папке с лабораторной. Называется "lab1.yaml".</li>
<li>Схема связи находится в папке с лабораторной. Называется "Схема.jpeg".</li>
</ul>
<h3>Текст конфигураций для сетевых устройств</h3>

<p>Для R01.TEST (sudo ssh admin@172.20.20.3):<br/></p>

<p>/interface vlan</p>
<p>add interface=ether2 name=vlan10 vlan-id=10</p>
<p>add interface=ether2 name=vlan20 vlan-id=20</p>
<p>/interface wireless security-profiles</p>
<p>set [ find default=yes ] supplicant-identity=MikroTik</p>
<p>/ip pool</p>
<p>add name=pool10 ranges=192.168.10.10-192.168.10.250</p>
<p>add name=pool20 ranges=192.168.20.10-192.168.20.250</p>
<p>/ip dhcp-server</p>
<p>add address-pool=pool10 disabled=no interface=vlan10 name=server10</p>
<p>add address-pool=pool20 disabled=no interface=vlan20 name=server20</p>
<p>/ip address</p>
<p>add address=172.31.255.30/30 interface=ether1 network=172.31.255.28</p>
<p>add address=192.168.10.1/24 interface=vlan10 network=192.168.10.0</p>
<p>add address=192.168.20.1/24 interface=vlan20 network=192.168.20.0</p>
<p>/ip dhcp-client</p>
<p>add disabled=no interface=ether1</p>
<p>/ip dhcp-server network</p>
<p>add address=192.168.10.0/24 gateway=192.168.10.1</p>
<p>add address=192.168.20.0/24 gateway=192.168.20.1</p>
<p>/system identity</p>
<p>set name=R01.TEST</p>

<p>Для SW01.L3.01.TEST (sudo ssh admin@172.20.20.4):<br/></p>

<p>/interface bridge</p>
<p>add name=bridge10</p>
<p>add name=bridge20</p>
<p>/interface vlan</p>
<p>add interface=ether2 name=vlan10 vlan-id=10</p>
<p>add interface=ether2 name=vlan20 vlan-id=20</p>
<p>add interface=ether3 name=vlan103 vlan-id=10</p>
<p>add interface=ether4 name=vlan203 vlan-id=20</p>
<p>/interface wireless security-profiles</p>
<p>set [ find default=yes ] supplicant-identity=MikroTik</p>
<p>/interface bridge port</p>
<p>add bridge=bridge20 interface=vlan20</p>
<p>add bridge=bridge20 interface=vlan203</p>
<p>add bridge=bridge10 interface=vlan103</p>
<p>add bridge=bridge10 interface=vlan10</p>
<p>/ip address</p>
<p>add address=172.31.255.30/30 interface=ether1 network=172.31.255.28</p>
<p>/ip dhcp-client</p>
<p>add disabled=no interface=ether1</p>
<p>add disabled=no interface=bridge10</p>
<p>add disabled=no interface=bridge20</p>
<p>/system identity</p>
<p>set name=SW01.L3.01.TEST</p>

<p>Для SW02.L3.01.TEST (sudo ssh admin@172.20.20.7):<br/></p>
<p>/interface bridge</p> 
<p>add name=bridge10</p> 
<p>/interface vlan</p> 
<p>add interface=ether2 name=vlan10 vlan-id=10</p> 
<p>/interface wireless security-profiles</p> 
<p>set [ find default=yes ] supplicant-identity=MikroTik</p> 
<p>/interface bridge port</p> 
<p>add bridge=bridge10 interface=vlan10</p> 
<p>add bridge=bridge10 interface=ether3</p> 
<p>/ip address</p> 
<p>add address=172.31.255.30/30 interface=ether1 </p><p>network=172.31.255.28</p> 
<p>/ip dhcp-client</p> 
<p>add disabled=no interface=ether1</p> 
<p>add disabled=no interface=bridge10</p> 
<p>/system identity</p> 
<p>set name=SW02.L3.01.TEST</p>

<p>Для SW02.L3.02.TEST (sudo ssh admin@172.20.20.5):<br/></p>
<p>/interface bridge</p> 
<p>add name=bridge20</p> 
<p>/interface vlan</p> 
<p>add interface=ether2 name=vlan20 vlan-id=20</p> 
<p>/interface wireless security-profiles</p> 
<p>set [ find default=yes ] supplicant-identity=MikroTik</p> 
<p>/interface bridge port</p> 
<p>add bridge=bridge20 interface=vlan20</p> 
<p>add bridge=bridge20 interface=ether3</p> 
<p>/ip address</p> 
<p>add address=172.31.255.30/30 interface=ether1 </p><p>network=172.31.255.28</p> 
<p>/ip dhcp-client</p> 
<p>add disabled=no interface=ether1</p> 
<p>add disabled=no interface=bridge20</p> 
<p>/system identity</p> 
<p>set name=SW02.L3.02.TEST</p>


<h3>Результаты пингов, проверки локальной связности</h3>
<img src="1.png" alt="">
<img src="2.png" alt="">
<img src="3.png" alt="">

