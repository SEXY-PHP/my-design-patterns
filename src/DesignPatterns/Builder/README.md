# Builder and Composite

Рассмотрим сразу два паттерна Строитель и Компоновщик.

#### Проблема:

Мы хотим написать генератор классов, трейтов, интерфейсов.

#### Решение:

Для сбора файла с классом будет использовать объект строителя. Для класса, трейта, интерфейса
будет свой строитель. Строитель будет строить дерево токенов, строк, блоков которое потом мы
обойдем и получим на выход готовый файл.

##### Компоновщик (Composite):

Данный паттерн позволит нам собирать объекты в дерево. Это позволит работать с большим количеством
объектов как с одним объектом. Вызвав __toString у корневого элемента мы запусти цепочку вызовов
__toString по всему дереву.

Корень дерева - класс File. Он является коллекцией объектов PartInterface.

PartInterface - интерфейс части файла, который предоставляет публичный метод __toString.

Token - реализует PartInterface и является примитивной частью файла. К примеру ключевые слова:
namespace, class, extends, public и т.д. Или спец. символы: $, (, ), {, } и т.д.

Line - реализует LineInterface, который наследует PartInterface. Используется как коллекция
Token и StringPart. Содержит в себе части строки и обычно заканчивается токеном EndLineToken.
После вызова __toString должна получиться одна строка.

Block - реализует BlockInterface, который наследует PartInterface. Используется как коллекция
BlockInterface и LineInterface. Содержит в себе строки и блоки.

Template - реализует TemplateInterface, который наследует PartInterface. Используется как коллекция
PartInterface. Используется как шаблоны, например если элемент не может быть Line т.к.
должен быть частью этого Line и не может быть Token т.к. слишком большой, для того чтобы быть
токеном. Также можно содержать разные реализации стандартов кода т.к. никто не запрещает в шаблон
вставлять Line и Block объекты.

Структура дерева следующая:
```
File
  | Block
    | Line
      | Token
      | StringPart
    | Template
      | PartInterface
    | Token
    | StringPart
```

Никто не запрещает менять структуру т.к. все компоненты реализуют PartInterface и являются
взаимозаменяемыми. Каждая из реализаций лишь описывает часть файла для поддерживания
принципа единственной ответственности (The Single Responsibility Principle).

Как выполнен обход по дереву?

Все коллекции компилируют строку делегируя выполнение __toString своим дочерним элементам.
При вызове __toString коллекция циклом вызывает __toString у дочерних элементов и результат добавляет
в конец общей строки и возвращает итоговую строку.

Конкретными исполнителями являются Token и StringPart. Они возвращают сразу строку из памяти.

Примем сборки дерева вручную написан в `client_code_manuly_build_composite.php`.

##### Плюсы:

🤩 Упрощает архитектуру клиента при работе со сложным деревом компонентов.
Прячем сложную структуру объектов в простой интерфейс, что упрощает структуру клиентского кода.

🤩 Легко добавляются новые виды компонентов.

##### Минусы:

🤔 Создаёт слишком общий дизайн классов.


##### Строитель (Builder):

Данный паттерн поможет нам спрятать сборку дерева внутри себя + ещё появляется возможность
автоматизировать сборку дерева вызывая нужные методы из билдера.

ClassBuilder - пример строителя обычного класса. Реализует интерфейсы ClassBuilderInterface,BuilderInterface,
Inheritance, MethodsWithBody, Properties. Внутри него спрятана логика по валидации и обработки
входящих параметров, который преобразуется в параметры для дерева.

Примем работы со строителем `client_code_with_builder.php`.

##### Директор (Director):

Является частью паттерна Строитель (Builder). Может содержать логику вызова методов у строителя
по входящим параметрам. То есть мы передаем директору строителя и параметры, а директор
возвращает готовый File. При этом мы на лету можем менять параметры и строителей.

Примем работы со строителем `client_code_with_director.php`.

##### Плюсы:

💃 Одно место для создания продуктов.

🕺 Можно создавать разные продукты.

💃 Позволяет выделить шаги сборки объекта.

💃 Прячем сложную сборку под простым интерфейсом.

##### Минусы:

🧐 Усложняет код из-за дополнительных классов.

🤯 Строители могут иметь разные интерфейсы, что заставляет клиента привязываться к корректной
реализации строителя.
