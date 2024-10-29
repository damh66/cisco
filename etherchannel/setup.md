# Настройка EtherChannel

### LACP

Режимы **LACP**:

- On
- Active
- Passive

<br/>

Таблица формирования канала **LACP**:

| S1 | S2 | Формирование канала |
|:----------:|:---------:|:---------:|
| ***On***  | ***On*** | ***Да*** |
| ***Active***  | ***Active/Passive***  | ***Да*** |
| On/Active/Passive | Off | Нет |
| On | Active | Нет |
| Passive/On | Passive | Нет |

<br/>

Конфигурация **LACP** на ***S1***:
```
interface range GigabitEthernet0/0/0-3
  channel-group 1 mode active
!
interface port-channel 1
  switchport trunk encapsulation dot1q
  switchport mode trunk
```
Конфигурация **LACP** на ***S2***:
```
interface range GigabitEthernet0/0/0-3
  channel-group 1 mode passive
!
interface port-channel 1
  switchport trunk encapsulation dot1q
  switchport mode trunk
```

<br/>

### PAgP

Режимы **PAgP**:

- On
- Desirable
- Auto

Таблица формирования канала **PAgP**:

| S1 | S2 | Формирование канала |
|:----------:|:---------:|:---------:|
| ***On***  | ***On*** | ***Да*** |
| ***Desirable***  | ***Desirable/Auto***  | ***Да*** |
| On/Desirable/Auto | Off | Нет |
| On | Desirable | Нет |
| Auto/On | Auto | Нет |

<br/>

Конфигурация **PAgP** на ***S1***:
```
interface range GigabitEthernet0/0/0-3
  channel-group 1 mode desirable
!
interface port-channel 1
  switchport trunk encapsulation dot1q
  switchport mode trunk
```
Конфигурация **PAgP** на ***S2***:
```
interface range GigabitEthernet0/0/0-3
  channel-group 1 mode auto
!
interface port-channel 1
  switchport trunk encapsulation dot1q
  switchport mode trunk
```
