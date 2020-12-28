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

<details><summary>пример ...</summary>

```java
import java.io.*;
import java.sql.*;
import java.util.Scanner;

public class OracleConnJDBC {
    static final String DATABASE_URL = "jdbc:oracle:thin:@localhost:1521/xe";
    static final String USER = "SCOTT";
    static final String PASSWORD = "tiger";
    static final String SQL = "Select empno, ename, to_char(hiredate, 'dd.mm.yyyy'), sal from emp";
    static final String file = "outfile.txt";
    static final String path = "./target/";

    public static void main(String[] args) {
        System.out.println("Инициализация драйвера и подключение к базе данных...");

        try (Connection conn = DriverManager.getConnection(DATABASE_URL, USER, PASSWORD);
             Statement stmt = conn.createStatement();
             FileWriter fout = new FileWriter(path + file)) {

           System.out.println("\nВыборка данных из таблицы в консоль:");
           ResultSet rslt = stmt.executeQuery(SQL);

           while(rslt.next()) {
              int empno = rslt.getInt(1);
              String ename = rslt.getString(2);
              String hiredate = rslt.getString(3);
              double sal = rslt.getDouble(4);
              System.out.println(empno + " " + ename + "\t" + hiredate + "\t" + sal);
              fout.write(empno + " " + ename + "\t" + hiredate + "\t" + sal + "\n");
           }

            System.out.println("\nДанные выборки успешно записаны в файл: " + path + file);

            rslt.close(); // Закрытие результирующего набора JDBC
            conn.close(); // Закрытие соединения с БД

        } catch (SQLException e) {
            System.out.println(e.getMessage());
        } catch (IOException e) {
            System.out.println(e.getStackTrace());
        }

        System.out.println("\nЧитаем файл (" + file + ") и выводим в консоль:" );
        try (FileReader reader = new FileReader(path + file);
             Scanner scan = new Scanner(reader))
        {
            while (scan.hasNextLine()) {
                System.out.println(scan.nextLine());
            }
        } catch (IOException e) {
            e.getStackTrace();
        }
    }
}

/* --------------------------------------------------
Инициализация драйвера и подключение к базе данных...
Выборка данных из таблицы в консоль:
7369 SMITH	17.12.1980	800.0
7499 ALLEN	20.02.1981	1600.0
7521 WARD	22.02.1981	1250.0
7566 JONES	02.04.1981	2975.0
7654 MARTIN	28.09.1981	1250.0
7698 BLAKE	01.05.1981	2850.0
7782 CLARK	09.06.1981	2450.0
7788 SCOTT	09.12.1982	3000.0
7839 KING	17.11.1981	5000.0
7844 TURNER	08.09.1981	1500.0
7876 ADAMS	12.01.1983	1100.0
7900 JAMES	03.12.1981	950.0
7902 FORD	03.12.1981	3000.0
7934 MILLER	23.01.1982	1300.0
Данные выборки успешно записаны в файл: ./target/outfile.txt
Читаем файл (outfile.txt) и выводим в консоль:
7369 SMITH	17.12.1980	800.0
7499 ALLEN	20.02.1981	1600.0
7521 WARD	22.02.1981	1250.0
7566 JONES	02.04.1981	2975.0
7654 MARTIN	28.09.1981	1250.0
7698 BLAKE	01.05.1981	2850.0
7782 CLARK	09.06.1981	2450.0
7788 SCOTT	09.12.1982	3000.0
7839 KING	17.11.1981	5000.0
7844 TURNER	08.09.1981	1500.0
7876 ADAMS	12.01.1983	1100.0
7900 JAMES	03.12.1981	950.0
7902 FORD	03.12.1981	3000.0
7934 MILLER	23.01.1982	1300.0
 */
  ```
 
</details>
