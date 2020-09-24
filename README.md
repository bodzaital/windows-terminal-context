# windows-terminal-context
Adds a right-click context item "Open a terminal here"

## How to use

Before installing the registry keys, edit the file so the keys are correctly set up.

```
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\Directory\Background\shell\windowsterminal]
@="Open a terminal here"
"Extended"=""
"Icon"=""

[HKEY_CLASSES_ROOT\Directory\Background\shell\windowsterminal\command]
@="\"C:\\Users\\{USERNAME}\\AppData\\Local\\Microsoft\\WindowsApps\\wt.exe\"-d \"%V\""
```

1. If you want to change the text that appears in the context menu, edit the string inside the quote marks: `@=""`
2. Download the [https://github.com/microsoft/terminal/blob/master/res/terminal.ico](official icon) from the Windows Terminal repo and place it somewhere, then set the path to the icon.
3. Change `{USERNAME}` to your actual username.

Then double click the `.reg` file and test it out by shift + right clicking in a directory. A new entry in the context menu, `Open a terminal here` or whatever you set, will appear.
If you don't want to hold shift while right clicking, remove the line `"Extended"=""`.

## What this does

Adds a new entry called `windowsterminal` to the registry in `HKEY_CLASSES_ROOT\Directory\Background\shell`, then adds three keys to this entry, a default `@` that is the text, an empty key called `Extended` that sets the shift + right clicking behavior, and an `Icon` key that contains the path to the icon file.

Within the `windowsterminal` entry, it adds another entry called `command` with only the default key, `@` that contains the path to the Windows Terminal executable with the command line argument to set the working directory to the current directory.

## Uninstalling

Open the registry editor and navigate to `HKEY_CLASSES_ROOT\Directory\Background\shell` and remove the entry `windowsterminal`. 
