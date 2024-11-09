# Маршрутизация VLAN

### Router on a stick

Таблица адресации:

  | Подинтерфейс | VLAN | IP-адрес |
  |:----------:|:---------:|:---------:|
  | G0/0/1.10 | 10 | 192.168.10.1/24 |
  | G0/0/1.20 | 20 | 192.168.20.1/24 |
  | G0/0/1.30 | 99 | 192.168.99.1/24 |

<br/>

Конфигурация **подинтерфейсов**:

   ```
   interface GigabitEthernet0/0/1.10
     encapsulation dot1Q 10
     ip address 192.168.10.1 255.255.255.0
   !
   interface GigabitEthernet0/0/1.20
     encapsulation dot1Q 20
     ip address 192.168.20.1 255.255.255.0
   !
   interface GigabitEthernet0/0/1.99
     encapsulation dot1Q 99
     ip address 192.168.99.1 255.255.255.0
   ```

<br/>

### L3 Switch

Таблица адресации:

  | Интерфейс VLAN | IP-адрес |
  |:----------:|:---------:|
  | vlan10 | 192.168.10.1/24 |
  | vlan20 | 192.168.20.1/24 |

<br/>

1. Создание **VLAN**:
   ```
   vlan10
     name LAN10
   !
   vlan20
     name LAN20
   ```

2. Создание **виртуальных** интерфейсов:
   ```
   interface vlan10
     ip add 192.168.10.1 255.255.255.0
     no shuthown
   !
   interface vlan20
     ip address 192.168.20.1 255.255.255.0
     no shuthown
   ```

3. Настройка **портов доступа**:
   ```
   interface GigabitEthernet1/0/1
     switchport mode access
     switchport access vlan 10
   !
   interface GigabitEtherenet1/0/2
     switchport mode access
     swtchport access vlan 20
   ```

4. Активация **IP-маршрутизации**:
   ```
   ip routing
   ```
