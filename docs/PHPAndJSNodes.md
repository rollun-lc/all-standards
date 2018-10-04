# rollun-datastore vs rollun-rql: сравнение имплпементации RQL

## Ноды общего назначения
| PHP ноды | JS ноды | комментарий |
|----------|---------|-------------|
| limit(limit,offset) | limit(limit,offset,maxCount) |
| sort(+/-property) | sort(+/-property) |
| in(property,(value1,value2,...)) | in(property,(value1,value2...)) | Регистрозависима в DbTable, регистронезависима в jsArray и СSV
| out(property,(value1,value2,...)) |out(property,(value1,value2,...) )|
| and | and |
| not | not |
| or | or |
| eq | eq |
| ge | ge |
| gt | gt |
| le | le |
| lt | lt |
| ne | ne |
|| match | Поиск по RegExp
|groupby(property,property...) ||
||first| first record of the query's result set
||one| first and only record of the query's result set, or produces an error if the query's result set has more or less than one record in it.
||distinct() | result set with duplicates removed
||values(property) | Returns an array of the given property value for each object
| *`like`* |* like *|
| *`alike`* |* alike *|

## Аггрегатные ноды
| PHP ноды | JS ноды | комментарий |
|----------|---------|-------------|
| select(field1,field2,...) | select(field1,field2,...) |
| min(property) | min(property?) | в jsArray возвращает чисто значение вместо обьекта со значениями;  в jsArray не работает через select()
| max(property) | max(property?) | в jsArray возвращает чисто значение вместо обьекта со значениями;  в jsArray не работает через select()
| count(property) | count(property?) | в jsArray возвращает чисто значение вместо обьекта со значениями;  в jsArray не работает через select()
| avg(property) | mean(property?) | в jsArray возвращает чисто значение вместо обьекта со значениями;  в jsArray не работает через select()
| sum(property) | sum(property?) | в jsArray возвращает чисто значение вместо обьекта со значениями;  в jsArray не работает через select()
| aggregateSelect ||Select с другим именем, работает для аггрегатных нод
## Ноды для работы с древовидными данными

| PHP ноды | JS ноды | комментарий |
|----------|---------|-------------|
||recurse(property?) | Recursively searches, looking in children of the object as objects in arrays in the given property value
|| contains(field,value) |Filters for objects where the specified property's value is an array and the array contains any value that equals the provided value or satisfies the provided expression.
||excludes(field,value/expression) (for array type)|Filters for objects where the specified property's value is an array and the array does not contain any of value that equals the provided value or satisfies the provided expression.
||rel(relation_name,query)| (**Непонятно, что она должна делать. Реализации на JS нет**) Applies the provided query against the linked data of the provided relation name.

## 'like', 'alike', 'match', 'contains': ожидания vs реальность

| Имя ноды | Реализация по спеке | Реализация PHP | Реализация JS |Комментарии|
|----------|---------------------|----------------|---------------|-----------|
|`like`|регистрочувствительный поиск с метасимволами (* - любое кол-во символов, ? - один)|В CSV и Memory - регистронезависимый поиск с метасимволами. В DbTable - зависит от настроек соединения с БД/SQL сервера/отдельной таблицы в бд|Работает согласно спеке |DbTable datastore возвращает цифры в виде строк, а CSV/Memory - в виде цифр
|`alike`|Регистронезависимый поиск с метасимволами (* - любое кол-во символов, ? - один)|Не реализована на PHP|Работает согласно спеке |
|`match`|Поиск по регулярному выражению|Является alias'ом на like|Работает согласно спеке | В скором времени нода будет обьявлена нежелательной
|`contains`|Поиск значений в древовидной структуре|Не работает с деревьями; предсталвяет из себя регистронезависимый `like`|Работает согласно спеке |
|`excludes`|Отрицающий поиск значений в древовидной структуре|не реализовано|Работает согласно спеке |