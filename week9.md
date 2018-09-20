# Technique

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
  
## Java Regexp Replace

```Java
"?name,?name,".reqlaceAll("\\?[^,]+", "tian")
```

## [guava charmatcher](https://github.com/google/guava/wiki/StringsExplained#charmatcher)

```Java
CharMatcher.anyOf(",").trimFrom(",a,b,,c,) // return a,b,,c
```
