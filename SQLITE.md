# Sqlite tutorial

## Documentation

* [Start here](http://www.sqlite.org/docs.html)
* [FAQ](http://www.sqlite.org/faq.html)
* [Command](http://www.sqlite.org/lang.html)
* [C/C++ API](http://www.sqlite.org/c3ref/funclist.html)
* [Command line shell](http://www.sqlite.org/sqlite.html)

## Tutorials

* [Tutorial](http://souptonuts.sourceforge.net/readme_sqlite_tutorial.html)
* [Sqlite Hammer](http://www.squidoo.com/sqlitehammer)
* [Squido tutorial](http://www.squidoo.com/sqlitetutorial)

## Tools

* [Tools](http://sb2.info/commercial-and-freeware-sqlite-tools-list-2/)
* [SQLiteman] (http://sqliteman.com/)

## sqlite3 commands and scripts

        .help
        .read ins_artists.sql
        .tables
        .schema
        .dump
        .quit
        .exit

## no DECODE or NVL, but IFNULL and CASE

        .header on

        CREATE TABLE testTable (id NUMBER);
        INSERT INTO testTable (Id) VALUES (1);
        INSERT INTO testTable (Id) VALUES (2);
        COMMIT;

        SELECT id
               ,(SELECT id
                   FROM testTable v2
                  WHERE v2.id = v.id)                  id2
               ,IFNULL(v.id, -1)                       n1
               ,IFNULL(NULL, v.id)                     n2
               ,CASE ID
                  WHEN 1 THEN 'first case'
                  WHEN 2 THEN 'second case'
                  ELSE 'Unknown case'
                END                                     CaseSample
              ,'EOT'                                    eot
        FROM testTable v
        WHERE Id IN (1, 2);

produces

        id|id2|n1|n2|CaseSample|eot
        1|1|1|1|first case|EOT
        2|2|2|2|second case|EOT

## no SYSDATE, but datetime('NOW')

        SELECT datetime('now') from testTable;

## no ROWNUM for limiting rows, but LIMIT

        SELECT id from testTable LIMIT 3;


## Types of columns. Is there sqlite_describe_column like OCIDescribeAny?

Possible candidates:
* typeof - SQL function
* sqlite3_column_type           - C api
* sqlite3_table_column_metadata - C api
* pragma table_info(testTable)

        SELECT name, sql FROM sqlite_master WHERE type='table' AND name = 'testTable';

There is no sqlite_describe_column which can provide to a host language the type which is required when you want to set the buffer of simple host type like integer, float, char[200].
Column can contain any value. This is a feature not a bug.

        SELECT id
               ,(SELECT id
                   FROM testTable v2
                  WHERE v2.id = v.id)                  id2
               ,IFNULL(v.id, -1)                       n1
               ,IFNULL(NULL, v.id)                     n2
               ,CASE ID
                  WHEN 1 THEN 'first case'
                  WHEN 2 THEN 'second case'
                  ELSE 'Unknown case'
                END                                     CaseSample
              ,typeof(id)                               TypeOfId
              ,typeof(CASE ID
                        WHEN 1 THEN 'first case'
                        WHEN 2 THEN 'second case'
                        ELSE 'Unknown case'
                      END asdfaaa)                      TypeOfCase
              ,typeof(CASE ID
                        WHEN 1 THEN NULL
                        WHEN 2 THEN 'second case'
                        ELSE 'Unknown case'
                      END)                             TypeOfCaseWithNull
              ,'EOT'                                    eot
         FROM testTable v
        WHERE Id IN (1, 2);

Possible to use pragma, however it does not give the type of
pragma table_info(testTable);

