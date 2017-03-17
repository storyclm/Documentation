# TablesQuery

**TablesQuery** - это язык запросов, разработанного специально для StoryCLM. 
Запрос в данном формате легко транслируется в любы другие языки запросов. 
Параметры из которых создается запрос могут быть двух типов: Comparison и Logical. 

### Comparison (операторы сравнения):

Оператор |	Тип поля для которого он применим     |	Пример запроса	              | Описание
---------|----------------------------------------|-------------------------------|---------------------------
[eq]	 | (string, int, double, bool, date)	  | [fieldname][eq]["value"]	  | Equals
[lt]	 | (int, double, date)	                  | [fieldname][lt][value]	      | Less Than operator
[lte]	 | (int, double, date)	                  | [fieldname][lte][value]	      | Less Than or Equal to operator
[gt]	 | (int, double, date)	                  | [fieldname][gt][value]	      | Greater Than operator
[gte]	 | (int, double, date)	                  | [fieldname][gte][value]	      | Greater Than or Equal to operator
[ne]	 | (string, int, double, bool, date)	  | [fieldname][ne]["value"]      | Not Equal to operator
[in]	 | (string, int, double, bool, date)	  | [fieldname][in]["val","val"]  |	Contained IN array operator
[nin]	 | (string, int, double, date)	          | [fieldname][nin]["val","val"] |	Not contained IN array
[cn]	 | (string)	                              | [fieldname][cn]["value"]	  | Contains
[re]	 | (string)	                              | [fieldname][re]["value"]	  | Regular Expression
[sw]	 | (string)	                              | [fieldname][sw]["value"]	  | Starts With
[ew]	 | (string)	                              | [fieldname][ew]["value"]	  | Ends With

### Logical (логические операторы): 

Используются для "соединения" несколько операторов сравнения операторов сравнения. Такие операторы могут располагаться только между операторами сравнения. Операторы сравнения стоящие в начале записи, в конце, соединяющие другие логические операторы, соединяющие логический оператор и оператор сравнения учитываться не будут.

Оператор  |	Тип поля для которого он применим	| Пример запроса
----------|-------------------------------------|--------------------------------------
[or]	  |(логический оператор)	            | [fieldname][eq]["value"][or][fieldname][eq]["value1"]
[and]	  |(логический оператор)	            | [fieldname][eq]["value"][and][fieldname][eq]["value1"]


### Примеры:

**Возраст меньше или равен 30**
```
[age][lte][30]
```
**Поле "name" начинается с символа "T"**
```
[name][sw]["T"]
```
**Поле "name" содержит строку "ad"**
```
[Name][cn]["ad"]
```
**Поиск имен из списка**
```
[Name][in]["Stanislav","Tamerlan"]
```
**Выбрать женщин, имя ("name") которых начинается со строки "V"**
```
[gender][eq][false][and][Name][sw]["V"]
```
**Выбрать мужчин младше 30 и женщин старше 30**
```
[gender][eq][true][and][age][lt][30][or][gender][eq][false][and][age][gt][30]
```
**Поле "name" начинается с символов "T" или "S" при этом возраст должен быть равен 22**
```
([name][sw]["S"][or][name][sw]["T"])[and][age][eq][22]
```
**Выбрать всех с возрастом НЕ в интервале [25,30] и с именами на "S" и "Т"**
```
([age][lt][22][or][age][gt][30])[and]([name][sw]["S"][or][name][sw]["T"])
```
 