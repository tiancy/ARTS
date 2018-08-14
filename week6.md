# Tip

## [safe update mode by mysql](https://stackoverflow.com/questions/11448068/mysql-error-code-1175-during-update-in-mysql-workbench)

Error Code: 1175. You are using safe update mode and you tried to update a table without a WHERE that uses a KEY column To disable safe mode, toggle the option in Preferences -> SQL Editor and reconnect.

Fixed Error

Try:

SET SQL_SAFE_UPDATES = 0;

Or you can modify your query to follow the rule (use primary key in where clause).

## Spring boot return html, annotated class is a "Controller", is not "RestController"

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

# Review

## [OSS CopyFile](https://help.aliyun.com/document_detail/32149.html?spm=a2c4g.11186623.6.765.wZWvY4#拷贝文件)

```Go
import "github.com/aliyun/aliyun-oss-go-sdk/oss"

client, err := oss.New("Endpoint", "AccessKeyId", "AccessKeySecret")
if err != nil {
    // HandleError(err)
}

bucket, err := client.Bucket("my-bucket")
if err != nil {
    // HandleError(err)
}

// oss file path
_, err = bucket.CopyObject("my-object", "descObjectKey")
if err != nil {
    // HandleError(err)
}
```
