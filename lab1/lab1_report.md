<p>University: [ITMO University](https://itmo.ru/ru/)</p>
<p>Faculty: [FICT](https://fict.itmo.ru)</p>
<p>Course: [Introduction in routing](https://github.com/itmo-ict-faculty/introduction-in-routing)</p>
<p>Year: 2022/2023 </p>
<p>Group: K33202</p>
<p>Author: Guliaeva Alisa</p>
<p>Lab: Lab1 </p>
<p>Date of create: 20.09.2022 </p>
<p>Date of finished: 18.11.2022</p>
<h1>Отчет по лабораторной №1</h1>
<h2>"Установка ContainerLab и развертывание тестовой сети связи"</h2>
<ul>
<li>Файл, который использовали для развертывания тестовой сети, находится в папке с лабораторной. Называется "lab1.yaml".</li>
<li>Схема связи находится в папке с лабораторной. Называется "Схема_сети.jpg".</li>
</ul>
<h3>Схема сети</h3>
<img src='Схема_сети.jpg' alt="">
<h3>Текст конфигураций для сетевых устройств</h3>

<h4>Для R01.TEST (sudo ssh admin@172.20.20.3)</h4>

<pre><code>
/interface vlan
add interface=ether2 name=vlan10 vlan-id=10
add interface=ether2 name=vlan20 vlan-id=20
/interface wireless security-profiles
set [ find default=yes ] supplicant-identity=MikroTik
/ip pool
add name=pool10 ranges=192.168.10.10-192.168.10.250
add name=pool20 ranges=192.168.20.10-192.168.20.250
/ip dhcp-server
add address-pool=pool10 disabled=no interface=vlan10 name=server10
add address-pool=pool20 disabled=no interface=vlan20 name=server20
/ip address
add address=172.31.255.30/30 interface=ether1 network=172.31.255.28
add address=192.168.10.1/24 interface=vlan10 network=192.168.10.0
add address=192.168.20.1/24 interface=vlan20 network=192.168.20.0
/ip dhcp-client
add disabled=no interface=ether1
/ip dhcp-server network
add address=192.168.10.0/24 gateway=192.168.10.1
add address=192.168.20.0/24 gateway=192.168.20.1
/system identity
set name=R01.TEST
</code></pre>

<h4>Для SW01.L3.01.TEST (sudo ssh admin@172.20.20.4)</h4>

<pre><code>
/interface bridge
add name=bridge10
add name=bridge20
/interface vlan
add interface=ether2 name=vlan10 vlan-id=10
add interface=ether2 name=vlan20 vlan-id=20
add interface=ether3 name=vlan103 vlan-id=10
add interface=ether4 name=vlan203 vlan-id=20
/interface wireless security-profiles
set [ find default=yes ] supplicant-identity=MikroTik
/interface bridge port
add bridge=bridge20 interface=vlan20
add bridge=bridge20 interface=vlan203
add bridge=bridge10 interface=vlan103
add bridge=bridge10 interface=vlan10
/ip address
add address=172.31.255.30/30 interface=ether1 network=172.31.255.28
/ip dhcp-client
add disabled=no interface=ether1
add disabled=no interface=bridge10
add disabled=no interface=bridge20
/system identity
set name=SW01.L3.01.TEST
</code></pre>

<h4>Для SW02.L3.01.TEST (sudo ssh admin@172.20.20.7)</h4>

<pre><code>
/interface bridge
add name=bridge10
/interface vlan
add interface=ether2 name=vlan10 vlan-id=10
/interface wireless security-profiles
set [ find default=yes ] supplicant-identity=MikroTik
/interface bridge port
add bridge=bridge10 interface=vlan10
add bridge=bridge10 interface=ether3
/ip address
add address=172.31.255.30/30 interface=ether1 network=172.31.255.28
/ip dhcp-client
add disabled=no interface=ether1
add disabled=no interface=bridge10
/system identity
set name=SW02.L3.01.TEST
</code></pre>

<h4>Для SW02.L3.02.TEST (sudo ssh admin@172.20.20.5)</h4>

<pre><code>
/interface bridge
add name=bridge20
/interface vlan
add interface=ether2 name=vlan20 vlan-id=20
/interface wireless security-profiles
set [ find default=yes ] supplicant-identity=MikroTik
/interface bridge port
add bridge=bridge20 interface=vlan20
add bridge=bridge20 interface=ether3
/ip address
add address=172.31.255.30/30 interface=ether1 network=172.31.255.28
/ip dhcp-client
add disabled=no interface=ether1
add disabled=no interface=bridge20
/system identity
set name=SW02.L3.02.TEST
</code></pre>


<h3>Результаты пингов, проверки локальной связности</h3>
<figcaption>Вывод ip-адресов, розданных DHCP-серверами</figcaption>
<img src="1.png" alt="">
<figcaption>Проверка доступности хостов</figcaption>
<img src="2.png" alt="">
<figcaption>Вывод ip-адреса устройства</figcaption>
<img src="3.png" alt="">

<h3>Вывод</h3>
<div>
В ходе работы был изучен инструмент ContainerLab, развернута тестовая сеть связи и настроено оборудование на базе Linux и RouterOS.
</div>

