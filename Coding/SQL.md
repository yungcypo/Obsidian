# SQL
SQL stands for *Structural Query Language*  
It's a language which is commonly used "to talk to Databases"  

Database is just a place to store some data  
To use Database, you need some kind of DBMS - Database Management System, just like MySQL, PostgreSQL, Oracle, ...  
Their job is to manage databases, but all of them will use SQL  
There will be some minor differences, nothing you can't Google :)  

Now this is just a short introduction to SQL by [YouTube tutorial by NetworkChuck](https://www.youtube.com/watch?v=xiUTqnI6xk8)  

# Installation
I will be using MariaDB on Linux  
In tutorial he uses MySQL, but it doesn't seem to be supported on Arch anymore  
It might say `mysql`, but under the hood it's actually `mariadb`  
You will also get warning that `mysql` deprecated  
MariaDB is drop-in replacement for MySQL, so everything that works on MySQL, should work on MariaDB as well  

```shell
yay -S mysql  # install mariadb on your system

sudo mysql_install_db --user=mysql --basedir=/usr --datadir=/var/lib/mysql  # some kind of magic
sudo systemctl enable mariadb  # enable system process on system startup
sudo systemctl start mariadb  # run system process right now
sudo systemctl status mariadb  # check if system process is running
```

To run `mariadb`, just enter the command `sudo mariadb`  
There might be problem with some TLS/SSL certificates, just run `mariadb` with `--skip-ssl`  flag  
```shell
sudo mariadb  # run mariadb
sudo mariadb --skip-ssl  # run mariadb without ssl
```

Right now, the command `mariadb` will work, because it's on localhost and we don't have any password set  
In the future, on more realistic projects, you might see something like `mysql -u root -h sql.myserver.com -P 3306 -p`, but that's not important right now  

**Before we start** - After every command in `mariadb`  you have to type the semicolon (`;`), otherwise it will think that "you are not done yet"  

# Databases
## Show databases
This one is very difficult command :)   
```sql
show databases;
```

You might see some defaults like this  
```text
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| test               |
+--------------------+
```

## Create databases
Just type `create database` and the name of the database after it  
```sql
create database coffee;
```

## Interact with database
After entering this command, we will set is as "active" (let's say) and now we can interact with it  
```sql
use coffee;
```

# Tables
Each database has it's tables, just line Excel file has it's Sheets  
Now, when we are using `coffee` database, because we typed `use coffee;` before  

## Show tables
This will show tables of our database  
At the very beginning, it will be empty  
```sql
show tables;
```

## Create table
To create new table, it's as simple as this  
Inside parentheses, you will put the names of the columns along with datatype it should store  
Columns (along with their datatypes) are separated with comma  
```sql
create table coffee_table (id int, name varchar(255), region varchar(255), roast varchar(255));
```

If you wonder, `varchar` is like a string, and the number after specifies it's maximal length  

## Describe table
Just simple `describe <table_name>` will show more about your table  
```sql
describe coffee_table  
```

The output will look something like this  
```text
+--------+--------------+------+-----+---------+-------+
| Field  | Type         | Null | Key | Default | Extra |
+--------+--------------+------+-----+---------+-------+
| id     | int(11)      | YES  |     | NULL    |       |
| name   | varchar(255) | YES  |     | NULL    |       |
| region | varchar(255) | YES  |     | NULL    |       |
| roast  | varchar(255) | YES  |     | NULL    |       |
+--------+--------------+------+-----+---------+-------+
4 rows in set (0,001 sec)
```

## Inserting into table
```sql
insert into coffee_table values (1, "default route", "ethiopia", "light");
```

## Showing the actual table
```sql
select * from coffee_table;
```

The output will look something like this  
```text
+------+---------------+----------+-------+
| id   | name          | region   | roast |
+------+---------------+----------+-------+
|    1 | default route | ethiopia | light |
+------+---------------+----------+-------+
1 row in set (0,000 sec)
```

After adding other rows, it might look like this  
```text
+------+---------------+----------+----------+
| id   | name          | region   | roast    |
+------+---------------+----------+----------+
|    1 | default route | ethiopia | light    |
|    2 | docker run    | mexico   | medium   |
|    3 | helpdesk      | honduras | medium   |
|    3 | on-call       | peru     | dark     |
|    3 | ifconfig      | tanzania | blode    |
|    3 | traceroute    | bali     | med-dark |
+------+---------------+----------+----------+
```

Or another example   
```sql
select * from avengers;
```

Will look like
```text
+------+------------+-----------+----------+------+-------------------+
| id   | first_name | last_name | origin   | age  | alias             |
+------+------------+-----------+----------+------+-------------------+
|    1 | thor       | odison    | asgard   | 1500 | strongest avenger |
|    2 | clint      | barton    | earth    |   35 | hawkeye           |
|    3 | tony       | stark     | earth    |   52 | iron man          |
|    4 | peter      | parker    | earth    |   17 | spiderman         |
|    5 | groot      | groot     | planet x |   18 | tree              |
+------+------------+-----------+----------+------+-------------------+
```

### Showing only selected columns
Selecting just one column  
```sql
select name from coffee_table;
```  
```text
+---------------+
| name          |
+---------------+
| default route |
| docer run     |
| helpdesk      |
| on-call       |
| ifconfig      |
| traceroute    |
+---------------+
```

Selecting multiple columns  
```sql
select id, name from coffee_table;
```  
```text
+------+---------------+
| id   | name          |
+------+---------------+
|    1 | default route |
|    2 | docer run     |
|    3 | helpdesk      |
|    3 | on-call       |
|    3 | ifconfig      |
|    3 | traceroute    |
+------+---------------+
```

## Showing only selected rows
For example, showing only avengers that are from earth  
```sql
select * from avengers where origin = "earth";
```

```text
+------+------------+-----------+--------+------+-----------+
| id   | first_name | last_name | origin | age  | alias     |
+------+------------+-----------+--------+------+-----------+
|    2 | clint      | barton    | earth  |   35 | hawkeye   |
|    3 | tony       | stark     | earth  |   52 | iron man  |
|    4 | peter      | parker    | earth  |   17 | spiderman |
+------+------------+-----------+--------+------+-----------+
```

```sql
select * from avengers where origin = "earth" or origin = "asgard";
```

```text
+------+------------+-----------+--------+------+-------------------+
| id   | first_name | last_name | origin | age  | alias             |
+------+------------+-----------+--------+------+-------------------+
|    1 | thor       | odison    | asgard | 1500 | strongest avenger |
|    2 | clint      | barton    | earth  |   35 | hawkeye           |
|    3 | tony       | stark     | earth  |   52 | iron man          |
|    4 | peter      | parker    | earth  |   17 | spiderman         |
+------+------------+-----------+--------+------+-------------------+
```

```sql
select * from avengers where not origin = "earth";
```

```text
+------+------------+-----------+----------+------+-------------------+
| id   | first_name | last_name | origin   | age  | alias             |
+------+------------+-----------+----------+------+-------------------+
|    1 | thor       | odison    | asgard   | 1500 | strongest avenger |
|    5 | groot      | groot     | planet x |   18 | tree              |
+------+------------+-----------+----------+------+-------------------+
```

```sql
select alias from avengers where age < 30;
```

```text
+-----------+
| alias     |
+-----------+
| spiderman |
| tree      |
+-----------+
```

## Deleting from table
Our table right now  
```text
+------+------------+-----------+----------+------+-------------------+
| id   | first_name | last_name | origin   | age  | alias             |
+------+------------+-----------+----------+------+-------------------+
|    1 | thor       | odison    | asgard   | 1500 | strongest avenger |
|    2 | clint      | barton    | earth    |   35 | hawkeye           |
|    3 | tony       | stark     | earth    |   52 | iron man          |
|    4 | peter      | parker    | earth    |   17 | spiderman         |
|    5 | groot      | groot     | planet x |   18 | tree              |
|    6 | jeff       | smith     | earth    |   43 | jeff the man      |
+------+------------+-----------+----------+------+-------------------+
```

If we wanted to remove `jeff` (which doesn't belong here (which I definitely didn't add right now)), we can do this  
```sql
delete from avengers where first_name = "jeff";
```

**Warning!**  
Be careful what you delete, because you can't get it back  
You can delete a lot with one command  

## Update values in table  
`groot` shouldn't have a `last_name`, he's just `groot`  
```sql
update avengers set last_name = NULL where first_name = "groot";
```

Same as before, be careful what you do, you can overwrite valuable data  

## Selecting with order
You can display the table with it's values in order  
```sql
select * from avengers order by age asc;
```

> Note: `asc` stands for *"ascending"* and `desc` stands for *"descending"*  

```text
+------+------------+-----------+----------+------+-------------------+
| id   | first_name | last_name | origin   | age  | alias             |
+------+------------+-----------+----------+------+-------------------+
|    4 | peter      | parker    | earth    |   17 | spiderman         |
|    5 | groot      | NULL      | planet x |   18 | tree              |
|    2 | clint      | barton    | earth    |   35 | hawkeye           |
|    3 | tony       | stark     | earth    |   52 | iron man          |
|    1 | thor       | odison    | asgard   | 1500 | strongest avenger |
+------+------------+-----------+----------+------+-------------------+
```

## Altering table (add/remove columns)  
```sql
alter table avengers add beard boolean;
```  

We want to alter table - avengers table and we want to add there another column called beard which will store boolean datatype   

Now if we want to add to it, we can use `update` as shown before  
```sql
update avengers set beard = False;
update avangers set beard = True where first_name = "thor";
select * from avengers;
```

```text
+------+------------+-----------+----------+------+-------------------+-------+
| id   | first_name | last_name | origin   | age  | alias             | beard |
+------+------------+-----------+----------+------+-------------------+-------+
|    1 | thor       | odison    | asgard   | 1500 | strongest avenger |     1 |
|    2 | clint      | barton    | earth    |   35 | hawkeye           |     0 |
|    3 | tony       | stark     | earth    |   52 | iron man          |     0 |
|    4 | peter      | parker    | earth    |   17 | spiderman         |     0 |
|    5 | groot      | NULL      | planet x |   18 | tree              |     0 |
+------+------------+-----------+----------+------+-------------------+-------+
```