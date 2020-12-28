<small>
  
### Пример работы с Базой Данных Oracle через драйвер JDBC + Maven.

Maven + JDBC + Oracle

### Example of working with a Oracle Database using the ODBC driver + Maven.

>Для работы данного примера, необходимо установить [Oracle Database Express Edition (XE) Download](https://www.oracle.com/database/technologies/xe-downloads.html "Download")
>
Пример демонстрирует подключение к Базе Данных Oracle схема SCOTT и выполняет выборку из таблицы EMP. 
Полученный результат выводит на консоль и записывает по строкам в файл.
Далее читает по строкам этот файл и выводит на консоль.
  
[OracleConnJDBC - Пример работы с Базой Данных Oracle через драйвер JDBC](https://github.com/aykononov/Oracle_JDBC_Maven/tree/master/src/main/java/OracleConnJDBC.java "Посмотреть пример Java")

</small>

<details><summary>таблица ...</summary>
 ```sql
  create table EMP
(
  empno    NUMBER(4) not null,
  ename    VARCHAR2(10),
  job      VARCHAR2(9),
  mgr      NUMBER(4),
  hiredate DATE,
  sal      NUMBER(7,2),
  comm     NUMBER(7,2),
  deptno   NUMBER(2),
  add constraint PK_EMP primary key (EMPNO)
);
 ```
</details>
