# rollun-datastore vs rollun-rql: сравнение имплпементации RQL

## Ноды общего назначения

| PHP ноды | JS ноды | комментарий |
|----------|---------|-------------|
| limit(&lt;limit>,&lt;offset>) | limit(limit,offset,maxCount) |
| sort(+/-&lt;property>) | sort(+/-&lt;property>) |
| in(&lt;property>,(&lt;value1>,&lt;value2>,...)) | in(&lt;property>,(&lt;value1>,&lt;value2>...)) | Регистронезависима в DbTable
| out(&lt;property>,(&lt;value1?,&lt;value2>,...)) | out(&lt;property>,(&lt;value1?,&lt;value2>,...)) | Регистронезависима в DbTable
| and(&lt;node1>, &lt;node2>, ...) |and(&lt;node1>, &lt;node2>, ...) |
| or(&lt;node1>, &lt;node2>, ...) | or(&lt;node1>, &lt;node2>, ...) |
| eq(&lt;property>, &lt;value>)| eq(&lt;property>, &lt;value>) |
| ge(&lt;property>, &lt;value>) | ge(&lt;property>, &lt;value>) |
| gt(&lt;property>, &lt;value>) | gt(&lt;property>, &lt;value>) |
| le(&lt;property>, &lt;value>) | le(&lt;property>, &lt;value>) |
| lt(&lt;property>, &lt;value>) | lt(&lt;property>, &lt;value>) |
| ne(&lt;property>, &lt;value>) | ne(&lt;property>, &lt;value>) |
|| match | Поиск по RegExp;**DEPRECATED**
|groupby(&lt;property1>,&lt;property2>...) ||
||first()| first record of the query's result set
||one()| first and only record of the query's result set, or produces an error if the query's result set has more or less than one record in it.
||distinct() | result set with duplicates removed
||values(&lt;property>) | Returns an array of the given property value for each object
| not(&lt;node>) | not(&lt;node>) |
| *like(&lt;property>, &lt;value>)* | *like(&lt;property>, &lt;value>)* |Регистронезависима в DbTable
| *alike(&lt;property>, &lt;value>)* | *alike(&lt;property>, &lt;value>)* |
| *eqt(&lt;property>)* | *eqt(&lt;property>)* | property equals true
| *eqf(&lt;property>)* | *eqf(&lt;property>)* | property equals false
| *eqn(&lt;property>)* | *eqn(&lt;property>)* | property equals null

*Курсивом* выделены ноды, которые не входят в RQL по спецификации persvr/rql

## Аггрегатные ноды
| PHP ноды | JS ноды | комментарий |
|----------|---------|-------------|
| select(field1,field2,...) | select(field1,field2,...) |
| min(&lt;property>) | min(&lt;property?>?) |
| max(&lt;property>) | max(&lt;property?>?) |
| count(&lt;property>) | count(&lt;property?>?) |
| avg(&lt;property>) | mean(&lt;property?>?) |
| sum(&lt;property>) | sum(&lt;property?>?) |
| aggregateSelect ||Select с другим именем, работает для аггрегатных нод
## Ноды для работы с древовидными данными

| PHP ноды | JS ноды | комментарий |
|----------|---------|-------------|
||recurse(&lt;property?>?) | Recursively searches, looking in children of the object as objects in arrays in the given property value
||contains(&lt;field>,&lt;value>) |Filters for objects where the specified property's value is an array and the array contains any value that equals the provided value or satisfies the provided expression.
||excludes(&lt;field>,&lt;value/expression>) (for array type)|Filters for objects where the specified property's value is an array and the array does not contain any of value that equals the provided value or satisfies the provided expression.
||rel(&lt;relation_name,&lt;query>)| (**Непонятно, что она должна делать. Реализации на JS нет**) Applies the provided query against the linked data of the provided relation name.

## 'like', 'alike', 'match', 'contains': ожидания vs реальность

| Имя ноды | Реализация по спеке | Реализация PHP | Реализация JS |Комментарии|
|----------|---------------------|----------------|---------------|-----------|
|`like`|регистрозависимый поиск с метасимволами (* - любое кол-во символов, ? - один)|В CSV и Memory - регистронезависимый поиск с метасимволами. В DbTable - зависит от настроек соединения с БД/SQL сервера/отдельной таблицы в бд|Работает согласно спеке |DbTable datastore возвращает цифры в виде строк, а CSV/Memory - в виде цифр
|`alike`|Регистронезависимый поиск с метасимволами (* - любое кол-во символов, ? - один)|Не реализована на PHP|Работает согласно спеке |
|`match`|Поиск по регулярному выражению|Является alias'ом на like|Работает согласно спеке | В скором времени нода будет обьявлена нежелательной
|`contains`|Поиск значений в древовидной структуре|Не работает с деревьями; предсталвяет из себя регистронезависимый `like`|Работает согласно спеке |
|`excludes`|Отрицающий поиск значений в древовидной структуре|не реализовано|Работает согласно спеке |