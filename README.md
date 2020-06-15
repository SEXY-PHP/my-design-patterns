# Паттерны проектирования GOF

## Порождающие

- [Фабричный метод | Factory method](src/DesignPatterns/FactoryMethod)
- [Абстрактная фабрика | Abstract factory](src/DesignPatterns/AbstractFactory)
- [Строитель | Builder](src/DesignPatterns/Builder)
- [Прототип | Prototype](src/DesignPatterns/Prototype)
- [Одиночка | Singleton](src/DesignPatterns/Singleton)

## Структурные

- [Адаптер | Adapter](src/DesignPatterns/Adapter) - релизован совместно с Абстрактной фабрикой
- [Компоновщик | Composite](src/DesignPatterns/Builder) - рассматривается совместно со Строителем

## Поведенческие


### Отличия между паттернами

##### Фабричный метод - Шаблонный метод

`Фабричный метод` как частный случай `Шаблонного метода`.

##### Фабричный метод - Абстрактная фабрика

`Фабричный метод` воспроизводит продукт. `Абстрактная фабрика` воспроизводит
семейство продуктов и гарантирует, что все продукты воспроизведенные конкретной
фабрикой являются совместимыми.

##### Абстрактная фабрика - Строитель

`Абстрактная фабрика` занимается воспроизведение семейства продуктов. `Строитель` отвечает за построение
сложного объекта шаг за шагом.

##### Прототип - Фабричный метод

`Прототип` использует сложную операцию инициализации и не опирается на наследование.
`Фабричный метод` использует наследование и легкую инициализацию продукта.

##### Одиночка - Легковес

Если `Легковес` свел объект с внутренним состоянием до одного объекта, то он
будет напоминать `Одиночку`. Разница в том, что `Легковес` может в будущем
получить новое состояние и объектов станет больше чем один. Так-же объект `Легковес`
не может менять состояние внутри себя, `Одиночка` не запрещает менять своё
внутреннее состояние.

##### Адаптер - Мост

`Адаптер` меняет существующий интерфейс. `Мост` проектирует интерфейс общения
ядра с компонентами.

##### Адаптер - Декоратор - Заместитель - Фасад

`Адаптер` предоставляет альтернативный интерфейс для конкретного класса.
`Декоратор` предоставляет расширенный интерфейс, также поддерживает рекурсивную вложенность.
`Заместитель` не меняет интерфейс, а предоставляет точно такой же.
`Фасад` создает новый интерфейс для подсистемы классов.

##### Компоновщик - Декоратор

Оба паттерна имеют рекурсивную вложенность. `Декоратор` оборачивает только
один объект и предоставляет расширенный интерфейс. Узел `Компоновщик` может
иметь много объектов и узел никак не меняет интерфейс.
