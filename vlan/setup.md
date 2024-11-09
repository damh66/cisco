# Настройка VLAN

Создание **VLAN**:
```
vlan 10
  name student
```
<br/>

Назначение порта **VLAN**:
```
interface FastEthernet0/6
  switchport mode access
  switchport access vlan 10
```
<br/>

Создание и назначение **VLAN** для передачи данных и голоса:
```
vlan 20
  name student
!
vlan 150
  name voice
!
interface FastEthernet0/18
  switchport mode access
  switchport access vlan 20
  mls qos trust cos
  switchport voice vlan 150
```

<br/>
<br/>

Команды проверки **VLAN**:

| Команда | Описание |
|----------|---------|
| **show vlan brief** | Отображает имя, состояние и порты VLAN по одной VLAN на строку |
| **show vlan id** *vlan-id* | Отображает информацию об отдельной VLAN, определяемой по номеру идентификатора VLAN. Для vlan-id, диапазон идентификаторов VLAN: от 1 до 4094 |
| **show vlan** *name* | Отображает информацию об имени одной сети VLAN. Имя VLAN - это код ASCII размером от 1 до 32 символов |
| **show vlan summary** | Отображает общую информацию о VLAN |
