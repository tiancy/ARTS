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

## tail -- display the last part of a file

$ tail -f filename.log

## listening ports

lsof -i -P -n | grep LISTEN  

Refer to https://www.cyberciti.biz/faq/unix-linux-check-if-port-is-in-use-command/

## ps -- process status

ps -ef | grep java
