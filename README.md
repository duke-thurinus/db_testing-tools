# database_testing_tools

## User Guide
Install python3

Rename copy and rename config.ini.template to config.ini

Fill out server connection information in config.ini

For TESTFOLDERPATH place the absolute path of a folder you would like test files to be pulled from

Place tests in that folder (see Test File Construction for more details)

If the 2 stored procedures produce a semantically identical result the test will pass, if not the difference will be displayed

Run db_tester.py from the command line (Use the '-h' modifier to see additional options)

### Test File Construction
Test files are JSON in the this format:

```
[
	{
		"test name" : "",
		"procedure 1 name": "",
		"procedure 2 name": "",
		"arguments": []
	}
]
```

"test name" is a string, this name is arbitrary and for your tracking purposes.

"procedure 1 name" and "procedure 2 name" are strings for the names in the database of the 2 stored procedures you are testing against each other.

"arguments" are objects for the data that is being passed into the stored procedure. They follow this format:

```
{	
	"name": "",
	"type": "",
	"value":
}
```

Or

```
{
	"name": "",
	"type": "",
	"value": ,
	"interval": ""
}
```

Or

```
{
	"name": "",
	"type": "",
	"values": []
}
```

The name is the name of the argument as specified by the stored procedure. The arguments do not have to be listed in order.

Type specifies what data type the argument is and what format the value(s) need to be in. The currently supported data types are:

'INT' - The value must be an integer.

'DATETIME' - The value must be a string that SQL Server can parse into a DATETIME such as 'YYYY-MM-DD HH:MI:SS'.

'INTERVAL DATETIME' - The value must be an integer and the interval must be one of the following strings; 'year', 'quarter', 'month', 'dayofyear', 'day', 'week', 'weekday', 'hour', 'minute', 'second', 'millisecond'. This will pass into the stored procedure a DATETIME of the a number of the interval away from the current DATETIME equal to the value.

'TINTID' - The values must be a list of integers. It will pass into the stored procedure the user defined table tintIdType of the values.

## work todo
support string argument type

support .csv test files

support tests from sql files

use a db connection that is more compatible with pandas

clearer results on fail

include performance statistics (CPU time, read/writes)

flag empty results

expect same and expect different options
