# Настройка DHCPv4

### Конфигурация DHCPv4-сервера
1. Исключение IPv4-адресов:
   ```
   ip dhcp excluded address 192.168.10.1 192.168.10.10
   ```

2. Определение **имени пула**:
   ```
   ip dhcp pool DHCP_POOL
   ```

3. Настройка **параметров пула**:

  | Команда | Задача |
  |----------|:---------|
  | **network** *network-number* [mask / /prefix-lenght] | Определение пула адресов |
  | **default-router** *address* | Определение маршрутизатора или шлюза по умолчанию |
  | **dns-server** *address* | Назначение DNS-сервера |
  | **domain-name** *domain* | Назначение доменного имени |
  | **lease** *{days [hours [minutes]] / infinite}* | Определение срока DHCP-аренды |
  | **netbios-name-server** *address* | Определение сервера NetBIOS WINS |

<br/>

Пример конфигурации:
```
ip dhcp excluded-address 192.168.10.1 192.168.10.10
ip dhcp excluded-address 192.168.10.254
!
ip dhcp pool DHCP_POOL
  network 192.168.10.0 255.255.255.0
  default-router 192.168.10.1
  dns-server 192.168.11.5
  domain-name example.com
```

<br/>

### Конфигурация DHCPv4-клиента
Настройка интерфейса маршрутизатора на **получение** IP-адреса по **DHCP**:
```
interface GigabitEthernet0/0/1
  ip address dhcp
  no shutdown
```

<br/>

### Ретрансляция DHCP
Чтобы пересылать **широковещательные рассылки DHCPv4**, на  **Relay-агенте** требуется прописать команду ретрансляции на интерфейсе, который смотрит в сторону клиента:
```
interface GigabitEthernet0/0/0
  ip helper-address 192.168.10.1
```

<br/>

### Отключение и включение службы DHCPv4
Отключение **службы DHCPv4**:
```
no service dhcp
```

<br/>

Включение **службы DHCPv4**:
```
service dhcp
```

<br/>
<br/>

### Команды проверки DHCPv4-сервера

<table>
  <tr>
    <td align="center">Команда</td>
    <td align="center">Описание</td>
  </tr>
  <tr>
    <td><strong>show running-config | section dhcp</strong></td>
    <td>Отображает команды DHCPv4, настроенные на маршрутизаторе</td>
  </tr>
  <tr>
    <td><strong>show ip dhcp binding</strong></td>
    <td>Отображает список всех привязок IPv4 к MAC-адресам, предоставляемых сервисом DHCPv4</td>
  </tr>
  <tr>
    <td><strong>show ip dhcp server statistics</strong></td>
    <td>Отображает информацию о количестве принятых и отправленных сообщений DHCPv4</td>
  </tr>
</table>

