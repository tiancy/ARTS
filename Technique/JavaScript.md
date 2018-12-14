## Convert json to string
JSON.stringify({"name":"tian"})

## simplemde set value

```javascript
simplemde.value(text);
setTimeout(function() { simplemde.codemirror.refresh(); }, 2000);
```

## audio

```javascript
// set paused
$('audio').each(function() {
    this.currentTime = 0;
    this.pause();
});

// hide download control
<audio controlsList="nodownload"></audio>
```

## [ajaxSubmit](http://jquery.malsup.com/form/#options-object)

Empty file input elements are not handled correctly in ajaxSubmit, the empty element while ajaxSubmit() is missing Content-Type, server MultipartFile is null

solution add option
iframe: true

iframe
Boolean flag indicating whether the form should always target the server response to an iframe. This is useful in conjuction with file uploads. See the File Uploads documentation on the Code Samples page for more info. 
Default value: false
