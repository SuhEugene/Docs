# taxi.js

## Константы
- **RED** - красная ветка
- **YELLOW** - жёлтая ветка
- **GREEN** - зелёная ветка
- **BLUE** - синяя ветка
- **Point(name, x, z, line)** - возвращает объект `{name:string, x:int, z:int, line:int[0-3]}`

## class Taxi
**Переменные класса**
- **multiplier** - множитель стоимости. Общий метраж поездки умножается на него
- **pool** - mysql опрос, выдающий соеднинения

**Создание**
- Принимает два аргумента: **pool** и **multiplier** и устанавливает их как переменные класса
- Если **multiplier** не указан, то по умолчанию он `0.01`

Пример:
```js
const taxi = new Taxi(pool, 23)
```

**getPool()**
- Не принимает аргументов
- Возвращает __mysql connection__

Пример:
```js
taxi.getPool()
```

**setMultiplier(n)**
- Принимает один аргумент: **multiplier**
- Устанавливает его как переменную класса `multiplier`

Пример:
```js
taxi.setMultiplier(0.01)
```

**getDistance(A, B)**
- Принимает два аргумента: объекты **Point**
- Возвращает дистанцию между двумя точками

Пример:
```js
taxi.getDistance(Point('Name', 300, 0, RED), Point('Name2', 200, 200, GREEN))
```

## class Order
**Переменные класса**
- **user** - __Discord ID__ пассажира
- **taxist** - __Discord ID__ водителя
- **A** - **Point**, отправная точка
- **B** - **Point**, точка прибытия
- **distance** - расстояние между **A** и **B**
- **price** - цена, **disctance** умноженное на *Taxi.multiplier*

**Создание**
- Не принимает аргументов

Пример:
```js
const order = new Order()
```

**setUser(id)**
- Принимает один аргумент: __Discord ID__ пассажира
- Устанавливает его как переменную класса `user`

Пример:
```js
order.setUser(message.author.id)
```

**setTaxist(id)**
- Принимает один аргумент: __Discord ID__ водителя
- Устанавливает его как переменную класса `taxist`

Пример:
```js
order.setTaxist(message.author.id)
```

**setFrom(name)**
- Принимает один аргумент: Название точки назначения
- Устанавливает точку отправления. Обращается к базе данных взятой у *Taxi.getPool()*, запрашивает координаты точки с таким названием, при удаче устанавливает координаты как переменную класса `A` и возвращает `True`, при неудаче возвращает `False`

Пример:
```js
order.setFrom("Отсо")
```

**setTo(name)**
- Принимает один аргумент: Название точки назначения
- Устанавливает точку прибытия. Обращается к базе данных взятой у *Taxi.getPool()*, запрашивает координаты точки с таким названием, при удаче устанавливает координаты как переменную класса `B` и возвращает `True`, при неудаче возвращает `False`

Пример:
```js
order.setTo("Отсо")
```

**countPrice()**
- Не принимает аргументов
- Считает дистанцию между точками, устанавливает как переменную класса `distance`, умножает дистанцию на *Taxi.multiplier* и также устанавливает как переменную класса `price`

Пример:
```js
order.countPrice()
```
