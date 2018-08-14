# Tip

## Go

```Go
// [Monotonic Clocks](https://golang.google.cn/pkg/time/#hdr-Monotonic_Clocks)
start := time.Now()
... operation that takes 20 milliseconds ...
t := time.Now()
elapsed := t.Sub(start)

// [time format](https://stackoverflow.com/questions/20234104/how-to-format-current-time-using-a-yyyymmddhhmmss-format)
time.Now().Format("2006-01-02 15:04:05")

// Convert byte to string
string(byte[:])

// Convert string to int
strconv.Atoi(s)

// Convert interface to string
fmt.Sprint(...)
interfaceObj.(string)

// [mysql](https://github.com/go-sql-driver/mysql/)
import _ "github.com/go-sql-driver/mysql" //  go get -u github.com/go-sql-driver/mysql

sql.Open("mysql", "user:password@(address:port)/dbname")

// string to substring
str[strings.LastIndex(str, ","):]
```
