## vscode vim

Mac Setup

If key repeating isn't working for you, execute this in your Terminal, then restart VS Code.

```cmd
defaults write com.microsoft.VSCode ApplePressAndHoldEnabled -bool false         # For VS Code
defaults write com.microsoft.VSCodeInsiders ApplePressAndHoldEnabled -bool false # For VS Code Insider
defaults delete -g ApplePressAndHoldEnabled                                      # If necessary, reset global default
```

We also recommend going into System Preferences -> Keyboard and increasing the Key Repeat and Delay Until Repeat settings to improve your speed.

## [VSCode Clean the workspace directory](https://github.com/redhat-developer/vscode-java/wiki/Troubleshooting#clean-the-workspace-directory)

In some occasions, deleting the Java Language Server workspace directory is helpful to go back to a clean slate.

MacOS : $HOME/Library/Application Support/Code[ - Variant]/User/workspaceStorage/

Build failed, do you want to continue?
Problem solved I resolved this issue by clearing the workspace cache in VS code.

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
