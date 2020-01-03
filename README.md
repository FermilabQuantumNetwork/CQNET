# CQNET
Compilation of tips, notes, and useful commands for setting up and running the code from CQNET.


## Python
### Useful commands
To install python packages, use:
* `python -m pip install --user <package1> <package2> ...`
* `python3 -m pip install --user <package1> <package2> ...`


### Tips
* If you are on Centos 7, install tkinter to use graphical interface for viewing matplotlib plots:
`sudo yum install python3-tkinter`


## Mysql
### Useful commands

Angle bracket terms should be replaced with your inputs.

#### Login to mysql
These commands will prompt for password.

* From computer with database:
```
mysql -u root -p
```

* From computer in network:
```
mysql -u <username> -h '<IP address>' -p
```


#### Create database
```create database <database name>;```

#### Create user
```
create user '<username>'@'<IP address>'
	identified by '<password>';

grant all on *.*
	to '<username>'@'<IP address>'  
	with grant option;
```
* On terminal of computer with database:

```
grant all privileges on *.* to '<username>'@'<IP address>' with grant option;
flush privileges;
```

For more info, look up "MySQL 6.2.8 Adding Accounts, Assigning Privileges, and Dropping Accounts"
#### Drop user

```
drop user '<username>'@'<IP address>'
```


#### Create table
Example: create table called myTable with five columns and different datatypes.

```
create table myTable(id int not null primary key auto_increment,
                         Vmax0 float,
                         Vmax1 float,
                         Vmax2 float,
                         datetime datetime); //create a new table
```

#### Select single row of table
Example:

```
select *
from <table name>
where <primary key name> = 123;
```


#### Select multiple rows of table
Example:

```
select * from <table name> limit 55719,76063;
```

#### Rename table
```
ALTER TABLE <old_table> RENAME <new_table>;
```


#### Rename column of table

```
alter table <table name> rename column <old name> to <new name>;
```

#### Add column

```
ALTER TABLE table ADD [COLUMN] <column_name_1> <column_1_definition> [FIRST|AFTER existing_column];
```
The square bracket terms are optional.
