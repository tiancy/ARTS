
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

// string replace
// Replace returns a copy of the string s with the first n non-overlapping instances of old replaced by new. If old is empty, it matches at the beginning of the string and after each UTF-8 sequence, yielding up to k+1 replacements for a k-rune string. If n < 0, there is no limit on the number of replacements.
strings.Replace(s, old, new, n)

// TrimSpace returns a slice of the string s, with all leading and trailing white space removed, as defined by Unicode.
strings.TrimSpace(" \t\n Hello, Gophers \n\t\r\n")
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

## Go exec runs external commands for ffmpeg

```Go
cmd := exec.Command("/usr/local/bin/ffmpeg", "-i", inputUrl, "-ss", soundBegin, "-to", soundEnd, outputUrl)
cmd.run()
```

[ffmpeg](https://www.ffmpeg.org/ffmpeg.html#Automatic-stream-selection)

## Go Log

```Go
f, err := os.OpenFile(time.Now().Format("2006-01-02")+".log", os.O_RDWR | os.O_CREATE | os.O_APPEND, 0666)
if err != nil {
    log.Fatalf("error opening file: %v", err)
}
defer f.Close()

// just write file
log.SetOutput(f)

// write file and stdout
w := io.MultiWriter(os.Stdout, f)
log.SetOutput(w)

log.Println("This is a test log entry")
```
references
[SetOutput](https://golang.google.cn/pkg/log/#SetOutput)
[go-golang-write-log-to-file](https://stackoverflow.com/questions/19965795/go-golang-write-log-to-file)

## [Go Regexp ReplaceAllString](https://golang.org/pkg/regexp/#example_Regexp_ReplaceAllString)

```Go
re := regexp.MustCompile("guys")
re.ReplaceAllString("hi guys", "boy") // return hi boy
```

## [Go remove and mkdir](https://golang.google.cn/pkg/os/#Mkdir)

```Go
os.RemoveAll("temp")
os.Mkdir("temp", os.ModePerm)
```
