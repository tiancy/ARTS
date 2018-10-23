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

## JavaScript

* simplemde set value

```javascript
simplemde.value(text);
setTimeout(function() { simplemde.codemirror.refresh(); }, 2000);
```

* audio

```javascript
// set paused
$('audio').each(function() {
    this.currentTime = 0;
    this.pause();
});

// hide download control
<audio controlsList="nodownload"></audio>
```

# Share

## [ajaxSubmit](http://jquery.malsup.com/form/#options-object)

Empty file input elements are not handled correctly in ajaxSubmit, the empty element while ajaxSubmit() is missing Content-Type, server MultipartFile is null

solution add option
iframe: true

iframe
Boolean flag indicating whether the form should always target the server response to an iframe. This is useful in conjuction with file uploads. See the File Uploads documentation on the Code Samples page for more info. 
Default value: false
