# REST API

## Таблицы

### API requests

Название                                                                     |      HTTP Verb               |             Описание
-----------------------------------------------------------------------------|------------------------------|----------------------------------------------------------------
tables/{tableId:int}/count                                                   |        GET                   |    Получает колличество записей в таблице
tables/{tableId:int}/countbyquery/{query:tablesquery}                        |        GET                   |    Получает колличество записей в таблице по запросу
tables/{tableId:int}/logcount                                                |        GET                   |    Получает колличество записей в логе таблицы
tables/{tableId:int}/logcountbydate/{date:unixdate}                          |        GET                   |    Получает колличество записей лога таблицы после указанной даты
tables/{tableId:int}/log/{skip:int}/{take:int}                               |        GET                   |    Получает все записи лога таблицы
tables/{tableId:int}/logbydate/{skip:int}/{take:int}/{date:unixdate}         |        GET                   |    Получает все записи лога таблицы после указанной даты
tables/{tableId:int}/findall/{skip:int}/{take:int}                           |        GET                   |    Получает постранично все данные таблицы
tables/{tableId:int}/find/{query:tablesquery}/{sort:int}/{sortfieldname:string}/{skip:int}/{take:int} | GET  |    Получает постранично данные по запросу
tables/{tableId:int}/findbyid/{id:int}                                       |        GET                   |    Получает запись по идендификатору в таблице
tables/{tableId:int}//findbyids                                              |        GET                   |    Получает коллекцию записей по списку идендификаторов в таблице
tables/{tableId:int}/delete/{id:int}                                         |        DELETE                |    Удалить запись в таблице по идендификатору
tables/{tableId:int}/deletemany                                              |        DELETE                |    Удаляет записи таблицы по списку идендификаторов
tables/{tableId:int}/shema                                                   |        GET                   |    Получает схему таблицы
tables/{tableId:int}/tables                                                  |        GET                   |    Получает список таблиц доаступных пользователю
tables/{tableId:int}/insert                                                  |        POST                  |    Добавляет сущность в таблицу
tables/{tableId:int}/insertmany                                              |        POST                  |    Добавляет коллекцию сущностей с таблицу
tables/{tableId:int}/update                                                  |        PUT                   |    Перезаписывает запись целиком
tables/{tableId:int}/updatemany                                              |        PUT                   |    Перезаписывает группу записей



