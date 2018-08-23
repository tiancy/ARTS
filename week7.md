# Tip

## Go

```Go
// Monotonic Clocks
// reference https://golang.google.cn/pkg/time/#hdr-Monotonic_Clocks
start := time.Now()
... operation that takes 20 milliseconds ...
t := time.Now()
elapsed := t.Sub(start)

// time format
// reference https://stackoverflow.com/questions/20234104/how-to-format-current-time-using-a-yyyymmddhhmmss-format
time.Now().Format("2006-01-02 15:04:05")

// Convert reader to string
// reference https://stackoverflow.com/questions/9644139/from-io-reader-to-string-in-go
buf := new(bytes.Buffer)
buf.ReadFrom(Reader)
buf.String()

// Convert byte to string
//string(byte[:])
string(byte)

// Convert string to byte
[]byte(str)

// Convert string to int
strconv.Atoi(s)

// Convert interface to string
interfaceObj.(string) // if interfaceObj is nil, runtime error
fmt.Sprint(interfaceObj)

// mysql
// reference https://github.com/go-sql-driver/mysql/
import _ "github.com/go-sql-driver/mysql" //  go get -u github.com/go-sql-driver/mysql

sql.Open("mysql", "user:password@(address:port)/dbname")

// string to substring
str[strings.LastIndex(str, ","):]
```

## Go read file lines from GBK encoding convert to UTF-8

```Go
import (
  sc "golang.org/x/text/encoding/simplifiedchinese"
  "golang.org/x/text/transform"
)

file, err := os.Open("filepath")
if err != nil {
  log.Fatal(err)
}
defer file.Close()

scanner := bufio.NewScanner(file)

for scanner.Scan() {
  text := bytes.NewBufferString(scanner.Text())
  ntext := transform.NewReader(text, sc.GBK.NewDecoder())
  str, err := ioutil.ReadAll(ntext)
  if err != nil {
    log.Fatal(err)
  }

  fmt.Printf("%s\n", string(str[:]))
}
```

References

[https://golang.org/pkg/bufio/#example_Scanner_lines](https://golang.org/pkg/bufio/#example_Scanner_lines)

[https://gist.github.com/zhangbaohe/c691e1da5bbdc7f41ca5](https://gist.github.com/zhangbaohe/c691e1da5bbdc7f41ca5)

## Go json marshal

```Go
// Escape HTML in data, "<br/>" --> "\u003cbr/\u003e"
json.Marshal(data)

// It is not escape HTML in data,  "<br/>" --> "<br/>"
var buf bytes.Buffer
e := json.NewEncoder(&buf)
e.SetEscapeHTML(false)
e.Encode(data)

fmt.Println(buf.String())
```

Reference [https://play.golang.org/p/OG-LA9XTmAm](https://play.golang.org/p/OG-LA9XTmAm)
