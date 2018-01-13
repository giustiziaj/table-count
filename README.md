# table-count
script to count all records in each table in a mysql database

## Usage
`./table-count [options]`

| flag | long form  | function | default |
| ---- | ---------- | -------- | ------- |
| -h   | --help     | prints help text | N/A |
| -H   | --host     | hostname of the database | localhost |
| -p   | --port     | port number to use for the database | 3306 |
| -u   | --user     | username to login to database | current username |
| -d   | --database | database to connect to | N/A |

Output will be in the form
```
Table1: Count1
Table2: Count2
...
```
