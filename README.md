# -10-Python-OOP-Principles
## Принципы ООП Python
<img src="https://github.com/TeachKait20/NoneCode/blob/main/OOP+python+principles/mine-bee.gif?raw=true" width=200>

Объектно-ориентированное программирование (ООП) — это один из самых популярных подходов к разработке программного обеспечения. Он позволяет структурировать код, делая его более понятным, гибким и удобным для расширения. <br><br>
Главная идея ООП заключается в моделировании реального мира с помощью объектов — сущностей, которые объединяют в себе данные (атрибуты) и поведение (методы). Этот подход упрощает проектирование сложных систем и делает код более логичным и читаемым.
```python
class Bee:
    def __init__(self, name: str, speed: int):
        """Инициализация пчелы с именем и скоростью полета"""
        self.name = name  # имя пчелы
        self.speed = speed  # скорость в км/ч
        self.is_flying = False  # изначально пчела не летает

    def start_flying(self):
        """Пчела начинает летать"""
        if not self.is_flying:
            self.is_flying = True
            print(f"{self.name} взлетела и летит со скоростью {self.speed} км/ч!")
        else:
            print(f"{self.name} уже в воздухе.")

bee1 = Bee("Пчел", 10)
bee1.start_flying()
```
Принципы объектно-ориентированного программирования (ООП) — это фундаментальные концепции, определяющие подход к проектированию программного кода на основе объектов. <br><br>
Эти принципы формируют основу объектно-ориентированного подхода, обеспечивая гибкость и удобство разработки, а также помогая организовать взаимодействие между объектами. Они применяются в самых разных областях программирования — от простых скриптов до сложных корпоративных систем.

## Наследование

<img src="https://github.com/TeachKait20/NoneCode/blob/main/OOP+python+principles/mine-summer.gif?raw=true" width=400>

**Наследование** - Позволяет создавать новые классы на основе существующих, наследуя их свойства и методы.
Синтакис:
```python
class ParentClass:
    def method_parent(self):
        pass

class ChildClass(ParentClass):
    def method_child(self):
        pass

obj = ChildClass()
obj.method_parent()  # Метод родительского класса доступен в дочернем
obj.method_child()   # Метод дочернего класса

```
### Пример наследования 1
Допустим, у нас есть два устройства: телефон и ноутбук. У каждого из них есть единственный атрибут — модель или производитель.
```python
class Smartphone():
    def __init__(self, brand):
        self.brand = brand

    def make_call(self, number):
        print(f"{self.brand}: Звонок на номер {number}...")

class Laptop():
    def __init__(self, model):
        self.model = model

    def run_program(self, program):
        print(f"Ноутбук {self.model} запускает {program}.")


phone = Smartphone("Samsung")
phone.make_call("+7 900 123 45 67")

laptop = Laptop("MacBook Pro")
laptop.run_program("Visual Studio Code")
```
Вывод:
```
Samsung: Звонок на номер +7 900 123 45 67...
Ноутбук MacBook Pro запускает Visual Studio Code.
```
Код работает, но у устройств может быть общее поведение, например, возможность включаться и выключаться. Вместо того чтобы добавлять эти методы в каждый класс отдельно, создадим общий родительский класс `Device`, от которого унаследуем `Smartphone` и `Laptop`.
```python
class Device:
    def turn_on(self):
        print("Устройство включено.")

    def turn_off(self):
        print("Устройство выключено.")

class Smartphone(Device):
    def __init__(self, brand):
        self.brand = brand

    def make_call(self, number):
        print(f"{self.brand}: Звонок на номер {number}...")

class Laptop(Device):
    def __init__(self, model):
        self.model = model

    def run_program(self, program):
        print(f"Ноутбук {self.model} запускает {program}.")

phone = Smartphone("Samsung")
phone.turn_on()
phone.make_call("+7 900 123 45 67")
phone.turn_off()

laptop = Laptop("MacBook Pro")
laptop.turn_on()
laptop.run_program("Visual Studio Code")
laptop.turn_off()
```
Вывод:
```
Устройство включено.
Samsung: Звонок на номер +7 900 123 45 67...
Устройство выключено.

Устройство включено.
Ноутбук MacBook Pro запускает Visual Studio Code.
Устройство выключено.
```
### Пример наследования 2
Программа, моделирующая структуру сотрудников в компании.
```python
class Employee:
    """Базовый класс для сотрудников компании"""
    def __init__(self, name, position):
        self.name = name
        self.position = position

    def work(self):
        print(f"{self.name} работает на должности {self.position}.")

class Manager(Employee):
    """Класс менеджера, наследуется от Employee"""
    def __init__(self, name, department):
        super().__init__(name, "Менеджер")  # Наследуем атрибуты Employee
        self.department = department

    def manage(self):
        print(f"{self.name} управляет отделом {self.department}.")

# Создание экземпляров сотрудников
emp = Employee("Олег", "Разработчик")
emp.work()

mgr = Manager("Анна", "Продажи")
mgr.work()   # Наследованный метод
mgr.manage()  # Метод, уникальный для менеджера
```
* Базовый класс `Employee` задаёт общие свойства всех сотрудников (имя, должность).
* Дочерний класс `Manager` наследует `Employee`, но также получает дополнительный атрибут `department` и метод `manage()`.
* Конструкция `super` может наследовать атрибуты родительского класса. Использование `super()` позволяет `Manager` вызывать конструктор `Employee`, избегая дублирования кода.
* Создаются объекты обычного сотрудника (`emp`) и менеджера (`mgr`), после чего проверяется их функциональность.

## Инкапсуляция

<img src="https://github.com/TeachKait20/NoneCode/blob/main/OOP+python+principles/mine-autumn.gif?raw=true" width=400>

**Инкапсуляция** - это принцип, который подразумевает сокрытие деталей реализации класса и предоставление к ним доступа только через методы.
Синтакис:
```python
class Name_class:
    def __init__(self, atr1, atr2):
        self.atr1 = atr1
        self.__atr2 = atr2  # приватный атрибут

    def __private_method(self):  # приватный метод
        pass

    def public_method(self):
        self.__private_method()
        return self.__atr2

obj = Name_class('atr1', 'atr2')
obj.public_method()
# obj.__private_method() - ошибка
```

### Пример инкапсуляции 1
В реальном мире тоже существуют объекты с закрытыми методами. Например, холодильник. Как пользователи, мы можем только включить его в розетку, а затем он начнёт работать самостоятельно, без нашего вмешательства в его внутренние процессы.
```python
class Refrigerator:
    def __init__(self, color, brand):
        self.color = color
        self.brand = brand

    def __cold_on(self):
        print("Стало холоднее")

    def __freezer_on(self):
        print("Морозильная камера включилась")

    def turn_on(self):
        print("Холодильник включён в розетку")
        self.__cold_on()
        self.__freezer_on()

ref_1 = Refrigerator("Серый", "LG")
ref_1.turn_on()
# ref_1.__cold_on()  # Ошибка: метод __cold_on является приватным
```
Внутренние детали работы объекта скрыты от пользователя, и доступ к ним возможен только через публичные методы, как `turn_on()`.

### Пример инкапсуляции 2

