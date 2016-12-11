# REST API

## �������

### API requests

��������                                                                     |      HTTP Verb               |             ��������
-----------------------------------------------------------------------------|------------------------------|----------------------------------------------------------------
tables/{tableId:int}/count                                                   |        GET                   |    �������� ����������� ������� � �������
tables/{tableId:int}/countbyquery/{query:tablesquery}                        |        GET                   |    �������� ����������� ������� � ������� �� �������
tables/{tableId:int}/logcount                                                |        GET                   |    �������� ����������� ������� � ���� �������
tables/{tableId:int}/logcountbydate/{date:unixdate}                          |        GET                   |    �������� ����������� ������� ���� ������� ����� ��������� ����
tables/{tableId:int}/log/{skip:int}/{take:int}                               |        GET                   |    �������� ��� ������ ���� �������
tables/{tableId:int}/logbydate/{skip:int}/{take:int}/{date:unixdate}         |        GET                   |    �������� ��� ������ ���� ������� ����� ��������� ����
tables/{tableId:int}/findall/{skip:int}/{take:int}                           |        GET                   |    �������� ����������� ��� ������ �������
tables/{tableId:int}/find/{query:tablesquery}/{sort:int}/{sortfieldname:string}/{skip:int}/{take:int} | GET  |    �������� ����������� ������ �� �������
tables/{tableId:int}/findbyid/{id:int}                                       |        GET                   |    �������� ������ �� �������������� � �������
tables/{tableId:int}//findbyids                                              |        GET                   |    �������� ��������� ������� �� ������ ��������������� � �������
tables/{tableId:int}/delete/{id:int}                                         |        DELETE                |    ������� ������ � ������� �� ��������������
tables/{tableId:int}/deletemany                                              |        DELETE                |    ������� ������ ������� �� ������ ���������������
tables/{tableId:int}/shema                                                   |        GET                   |    �������� ����� �������
tables/{tableId:int}/tables                                                  |        GET                   |    �������� ������ ������ ���������� ������������
tables/{tableId:int}/insert                                                  |        POST                  |    ��������� �������� � �������
tables/{tableId:int}/insertmany                                              |        POST                  |    ��������� ��������� ��������� � �������
tables/{tableId:int}/update                                                  |        PUT                   |    �������������� ������ �������
tables/{tableId:int}/updatemany                                              |        PUT                   |    �������������� ������ �������



