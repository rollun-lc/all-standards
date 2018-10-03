## rollun-datastore nodes vs rollun-rql nodes comparison
| PHP Nodes | JS Nodes |comment|
|-----------|----------|-------|
| select(field1,field2,...) | select(field1,field2,...)|
| limit(limit,offset) | limit(limit,offset,maxCount) |
| sort(+/-field) | sort(+/-field)|
| in(property,(value1,value2,...)) | in(property,(value1,value2...))|
| out(property,(value1,value2,...)) |out(property,(value1,value2,...))|
| and | and|
| not | not|
| or | or |
| eq | eq |
| ge | ge |
| gt | gt |
| le | le |
| lt | lt |
| ne | ne |
| aggregateFunction(function,field) | sum(property?), mean(property?), max(property?), min(property?), count(property?)|
| aggregateSelect ||Select with another name
| like | match | Searches for exact value. 'match' explicitly converts to 'like' when working with rollun-datastore. Upper- and lowercase search in rollun-datastore depends on configuration of sql server which host the db.
| contains(field,value) | contains(field,value) | Searches for sequence of characters in value. Upper- and lowercase search in rollun-datastore depends on configuration of sql server which host the db.
||excludes(field,value/expression) (for array type)|
|groupby(field1,field2...) ||
||first| first record of the query's result set
||one| first and only record of the query's result set, or produces an error if the query's result set has more or less than one record in it.
||rel(relation_name,query)| Applies the provided query against the linked data of the provided relation name.
||recurse(property?) | Recursively searches, looking in children of the object as objects in arrays in the given property value
||distinct() | result set with duplicates removed
||values(property) | Returns an array of the given property value for each object

## 'like', 'alike', 'match', 'contains': ожидания vs реальность

| Имя ноды | Реализация по спеке | Реализация PHP | Реализация JS |Комментарии|
|----------|---------------------|----------------|---------------|-----------|
|`like`|регистрочувствительный поиск с метасимволами (* - любое кол-во символов, ? - один)|В CSV и Memory - регистронезависимый поиск с метасимволами. В DbTable - зависит от настроек соединения с БД/SQL сервера/отдельной таблицы в бд|Работает согласно спеке |DbTable datastore возвращает цифры в виде строк, а CSV/Memory - в виде цифр
|`alike`|Регистронезависимый поиск с метасимволами (* - любое кол-во символов, ? - один)|Не реализована на PHP|Работает согласно спеке |
|`match`|Поиск по регулярному выражению|Является alias'ом на like|Работает согласно спеке | В скором времени нода будет обьявлена нежелательной
|`contains`|Поиск значений в древовидной структуре|Не работает с деревьями; предсталвяет из себя регистронезависимый `like`|Работает согласно спеке |
|`excludes`|Отрицающий поиск значений в древовидной структуре|не реализовано|Работает согласно спеке |