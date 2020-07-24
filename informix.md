# Informix Injection Cheat Sheet

_source: [http://pentestmonkey.net/cheat-sheet/sql-injection/informix-sql-injection-cheat-sheet](http://pentestmonkey.net/cheat-sheet/sql-injection/informix-sql-injection-cheat-sheet)_

## Version
```
SELECT DBINFO('version', 'full') FROM systables WHERE tabid = 1;
SELECT DBINFO('version', 'server-type') FROM systables WHERE tabid = 1;
SELECT DBINFO('version', 'major'), DBINFO('version', 'minor'), DBINFO('version', 'level') FROM systables WHERE tabid = 1;
SELECT DBINFO('version', 'os') FROM systables WHERE tabid = 1; — T=Windows, U=32 bit app on 32-bit Unix, H=32-bit app running on 64-bit Unix, F=64-bit app running on 64-bit unix
```

## Comments
```
select 1 FROM systables WHERE tabid = 1; — comment
```

## Current User
```
SELECT USER FROM systables WHERE tabid = 1;
select CURRENT_ROLE FROM systables WHERE tabid = 1;
```

## List Users
```
select username, usertype, password from sysusers;
```

## List Password Hashes
```
TODO
```

## List Privileges
```
select tabname, grantor, grantee, tabauth FROM systabauth join systables on systables.tabid = systabauth.tabid; — which tables are accessible by which users
select procname, owner, grantor, grantee from sysprocauth join sysprocedures on sysprocauth.procid = sysprocedures.procid; — which procedures are accessible by which users
```

## List DBA Accounts
```
TODO
```

## Current Database
```
SELECT DBSERVERNAME FROM systables where tabid = 1; — server name
```

## List Databases
```
select name, owner from sysdatabases;
```

## List Columns
```
select tabname, colname, owner, coltype FROM syscolumns join systables on syscolumns.tabid = systables.tabid;
```

## List Tables
```
select tabname, owner FROM systables;
select tabname, viewtext FROM sysviews  join systables on systables.tabid = sysviews.tabid;
```

## List Stored Procedures
```
select procname, owner FROM sysprocedures;
```

## Find Tables From Column Name
```
select tabname, colname, owner, coltype FROM syscolumns join systables on syscolumns.tabid = systables.tabid where colname like '%pass%';
```

## Select Nth Row
```
select first 1 tabid from (select first 10 tabid from systables order by tabid) as sq order by tabid desc; — selects the 10th row
```

## Select Nth Char
```
SELECT SUBSTRING('ABCD' FROM 3 FOR 1) FROM systables where tabid = 1; — returns 'C'
```

## Bitwise AND
```
select bitand(6, 1) from systables where tabid = 1; — returns 0
select bitand(6, 2) from systables where tabid = 1; — returns 2
```

## ASCII Value -> Char
```
TODO
```

## Char -> ASCII Value
```
select ascii('A') from systables where tabid = 1;
```

## Casting
```
select cast('123′ as integer) from systables where tabid = 1;
select cast(1 as char) from systables where tabid = 1;
```

## String Concatenation
```
SELECT 'A' || 'B' FROM systables where tabid = 1; — returns 'AB'
SELECT concat('A', 'B') FROM systables where tabid = 1; — returns 'AB'
```

## String Length
```
SELECT tabname, length(tabname), char_length(tabname), octet_length(tabname) from systables;
```

## If Statement
```
TODO
```

## Case Statement
```
select tabid, case when tabid>10 then "High" else 'Low' end from systables;
```

## Avoiding Quotes
```
TODO
```

## Time Delay
```
TODO
```

## Make DNS Requests
```
TODO
```

## Command Execution
```
TODO
```

## Local File Access
```
TODO
```

## Hostname, IP Address
```
SELECT DBINFO('dbhostname') FROM systables WHERE tabid = 1; — hostname
```

## Location of DB files
```
TODO
```

## Default/System Databases
```
These are the system databases:
sysmaster
sysadmin*
sysuser*
sysutils*
```
