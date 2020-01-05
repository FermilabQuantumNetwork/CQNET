# CQNET
Compilation of tips, notes, and useful commands for setting up and running the code from CQNET.

## General Comments
* If the code doesn't run or asks for permission, you may need to run the script as root.

## Github
### Useful commands
* Check status of local repo: `git status`
* Switch branch: `git checkout <branch>`
* Store local changes: `git stash`
* Download files from branch called <branch> of github repo: `git pull origin <branch>`
* Add everything from local repo: `git add .`
* Commit with message <...>: `git commit -m <...>`
* Add + commit with message <...>: `git commit -a -m "<...>"`
* Upload commits from local repo to github repo: `git push`

### Tips
* If you forgot to pull before making local changes, you can save local changes, pull,
then revert to local changes by doing:
```
git stash
git pull origin <branch>
git stash pop
```
* Suggested order of commands to push local repo to github repo:
```
git status
git checkout <branch> //if necessary
git stash //to be safe
git pull //makes local repo same as github repo
git stash pop //updates the pulled repo with stashed changes
git add .
git commit -m "<Explanation of changes>"
git push
```

* If you get something like `warning: LF will be replaced by CRLF in <filename>.` in the terminal,
it's due to incompatible end of line specifications from different OS e.g. if uploaded code run on Linux
from a Windows computer or vice versa.
  - Unix: End of line represented with line feed (LF)
    - When you get code from git that was uploaded from a unix system they will only have an LF
    - Command to tell git to convert LF endings into CRLF
    when you checkout code: `git config --global core.autocrlf true`
  - Windows: End of line represented with carriage return (CR) and a line feed (LF) thus (CRLF)
    - When upload from windows, converts LF to CRLF
    - Command to tell git to convert CRLF to LF on commit,
    but not the other way around: `git config --global core.autocrlf input`


## Python
### Useful commands
#### Linux
* To install python packages on Linux terminal, use:
	- `python -m pip install --user <package1> <package2> ...`
	- `python3 -m pip install --user <package1> <package2> ...`

* To build python software on RHEL terminal:
```
	cd /usr/src/Python-3.7.3
	./configure --enable optimizations
	make altinstall
```

#### Windows
* To run different versions of python on Windows cmd, use:
	* `py -2` (python2)
	* `py -3` (python3)

* To install python packages on Windows, use:
	- `py -3 -m pip install <package name>` (python3)

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
