## cmd native2ascii -reverse filepath 

[native2ascii](https://native2ascii.net) Convert national language characters to and from their Unicode equivalents in plain ASCII text.

## set terminal color

export PS1="\[\e[30;1m\]\u@\h:\w\$\[\e[m\] " <br/>
alias ls='ls -G'

## decompression for jar file at cmd
 
$ unzip filename.jar [-d filepath]

$ jar tvf filename.jar // list for filename.jar

## [Searching for Commands in the History](http://www.gnu.org/software/bash/manual/html_node/Searching.html)

C-r

## [Cutting cmd](https://www.howtogeek.com/howto/ubuntu/keyboard-shortcuts-for-bash-command-shell-for-ubuntu-debian-suse-redhat-linux-etc/)

C-u

## logout ssh
C-d

## tail -- display the last part of a file

$ tail -100f filename.log

## listening ports

lsof -i -P -n | grep LISTEN  

Refer to https://www.cyberciti.biz/faq/unix-linux-check-if-port-is-in-use-command/

## ps -- process status

ps -ef | grep java

## linux chown, chmod
```
更改文件属主，也可以同时更改文件属组
chown [–R] 属主名 文件名
chown [-R] 属主名：属组名 文件名

$ chown tian tmp.log

r:4
w:2
x:1
$ chmod 770 tmp.log

```
Refer to https://www.w3cschool.cn/linux/linux-file-attr-permission.html

## mvn
mvn clean install -DskipTests

## linux whereis/which, 查看安装目录

whereis java

Refer to https://www.computerhope.com/unix/uwhereis.htm

## Sed

Sed是Stream EDitor的缩写，是Unix下常用的基于文件和管道的编辑工具，可以在手册中得到关于sed的详细信息。
编辑并不会改变源文件，sed只是处理源文件的每一行并 把结果显示在标准输出中（当然很容易使用重定向来定制）：

* sed ’s/^$/d’ file.go 删除所有空行
* sed ’s/^[ ]*$/d’ file.go 删除所有只包含空格或者制表符的行
* sed ’s/”//g’ file.go 删除所有引号
