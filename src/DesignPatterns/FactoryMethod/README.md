# Factory method

#### Проблема:

Нужен механизм кэширования с возможностью не изменяя написанный код добавлять новые хранилища
для хранения кэша.

#### Решение:

Написать такой код, который позволит подменять класс для работы с хранилищем. Для этого надо
определить интерфейс хранилища. Класс, который будет реализовывать PSR-16, будет иметь защищенный
фабричный метод возвращающий объект реализующий интерфейс хранилища.

Следующая структура позволит реализовать механизм кэширования со способностью расширятся
без модификации кода. Само расширение будет происходить через наследования. В наследуемом классе
будет переопределен фабричный метод, который будет возвращать новое хранилище.

##### Плюсы:

👌 Легкое добавление новых продуктов (в данном случае хранилищ) в систему.

👌 Реализует принцип открытости/закрытости (The Open Closed Principle).

👌 Класс избавлен от привязки к конкретной реализаций хранилищ.

👌 Производство продуктов (хранилищ) вынесено в одно место.

##### Минусы:

👎 При добавлении новых продуктов (хранилищ) надо добавлять создателя.