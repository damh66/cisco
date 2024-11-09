# Настройка SLAAC и DHCPv6

### Конфигурация SLAAC-сервера

Включение **IPv6-маршрутизации**:
```
ipv6 unicast-routing
```
> После этой команды маршрутизатор начнет рассылать **RA** сообщения
> > Требуется назначенный **IPv6-адрес** на интерфейсе маршрутизатора

<br/>

Назначение **IPv6-адреса** интерфейсу:
```
interface GigabitEthernet0/1
ipv6 address 2001:db8:acad:1::1/64
```

<br/>

### Конфигурация DHCPv6-сервера без отслеживания состояния

Включение **IPv6-маршрутизации**:
```
ipv6 unicast-routing
```

<br/>

Создание пула **DHCPv6** и указание параметров внутри него:
```
ipv6 dhcp pool IPV6-STATELESS
  dns-server 2001:db8:acad:1::254
  domain-name example.com
```

<br/>

**Привязка пула** к интерфейсу и **указание флага**:
```
interface GigabitEthernet0/0
  description Link to LAN
  ipv6 address fe80::1 link-local
  ipv6 address 2001:db8:acad:1::1/64
  ipv6 nd other-config-flag
  ipv6 dhcp server IPV6-STATELESS
```

<br/>

### Конфигурация DHCPv6-клиента без отслеживания состояния

Включение **IPv6-маршрутизации**:
```
ipv6 unicast-routing
```

<br/>

Настройка интерфейса:
```
interface GigabitEthernet0/0
  ipv6 enable
  ipv6 address autoconfig
```

<br/>

### Конфигурация DHCPv6-сервера с отслеживанием состояния

Включение **IPv6-маршрутизации**:
```
ipv6 unicast-routing
```

<br/>

Создание пула **DHCPv6** и указание параметров внутри него:
```
ipv6 dhcp pool IPV6-STATEFUL
  address prefix 2001:db8:acad:1::/64
  dns-server 2001:4860:4860::8888
  domain-name example.com
```

<br/>

**Привязка пула** к интерфейсу и **указание флага**:
```
interface GigabitEthernet0/0
  description Link to LAN
  ipv6 address fe80::1 link-local
  ipv6 address 2001:db8:acad:1::1/64
  ipv6 nd managed-config-flag
  ipv6 nd prefix default no-autoconfig
  ipv6 dhcp server IPV6-STATEFUL
```

<br/>

### Конфигурация DHCPv6-клиента с отслеживанием состояния

Включение **IPv6-маршрутизации**:
```
ipv6 unicast-routing
```

<br/>

Настройка интерфейса:
```
interface GigabitEthernet0/0
  ipv6 enable
  ipv6 address dhcp
```

<br/>

### Конфигурация маршрутизация в качестве агента ретрансляции DHCPv6

Настройка интерфейса:
```
interface GigabitEthernet0/0
  ipv6 address 2001:db8:acad:1::1/64
  ipv6 dhcp relay destination 2001:db8:acad:2::2 GigabitEthernet0/1
```
> Команда настраивается на интерфейсе, который смотрит в сторону клиентов DHCPv6 и указывает адрес сервера DHCPv6 с исходящим интерфейсом для доступа к серверу

<br/>
<br/>

### Команды проверки DHCPv6-сервера

| Команда | Описание |
|----------|---------|
| **show ipv6 dhcp pool** | Проверка имени DHCPv6-пула и его параметров. Команда также определяет количество активных клиентов |
| **show ipv6 dhcp binding** | Отображение локального адреса канала IPv6 клиента и глобального одноадресного адреса, назначенного сервером |
