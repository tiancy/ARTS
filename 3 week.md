## Tip

### [spring-boot hotswapping](https://docs.spring.io/spring-boot/docs/current/reference/html/howto-hotswapping.html)

### [mybatis #{name} vs ${name}](http://www.mybatis.org/mybatis-3/sqlmap-xml.html#select)

### mybatis like
* select column from table where column like concat(#{selectContent}, '%'), 查询条件中使用函数会影响性能
* select column from table where column like '${selectContent}%', 可能会导致sql注入

### git commit

git config --global core.editor /usr/bin/vim

### vscode vim

Mac Setup

If key repeating isn't working for you, execute this in your Terminal, then restart VS Code.

* defaults write com.microsoft.VSCode ApplePressAndHoldEnabled -bool false         # For VS Code
* defaults write com.microsoft.VSCodeInsiders ApplePressAndHoldEnabled -bool false # For VS Code Insider
* defaults delete -g ApplePressAndHoldEnabled                                      # If necessary, reset global default

We also recommend going into System Preferences -> Keyboard and increasing the Key Repeat and Delay Until Repeat settings to improve your speed.

