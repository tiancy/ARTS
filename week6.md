# Tip

## [safe update mode by mysql](https://stackoverflow.com/questions/11448068/mysql-error-code-1175-during-update-in-mysql-workbench)

Error Code: 1175. You are using safe update mode and you tried to update a table without a WHERE that uses a KEY column To disable safe mode, toggle the option in Preferences -> SQL Editor and reconnect.

Fixed Error

Try:

SET SQL_SAFE_UPDATES = 0;

Or you can modify your query to follow the rule (use primary key in where clause).

## Spring boot return html, annotated class is a "Controller", is not "RestController"

## Go
* [Monotonic Clocks by Go](https://golang.google.cn/pkg/time/#hdr-Monotonic_Clocks)

```Go
start := time.Now()
... operation that takes 20 milliseconds ...
t := time.Now()
elapsed := t.Sub(start)
```

* [Go time format](https://stackoverflow.com/questions/20234104/how-to-format-current-time-using-a-yyyymmddhhmmss-format)

time.Now().Format("2006-01-02 15:04:05")

* Convert byte to string

string(byte[:])

* Convert string to int

strconv.Atoi(s)

* Convert interface to string

fmt.Sprint(...)

## vscode snippets

Preferences -> User snippets
```Json
// Example:
"Print to console": {
  "prefix": "log",
  "body": [
    "console.log('$1');",
    "$2"
  ],
  "description": "Log output to console"
}
```
