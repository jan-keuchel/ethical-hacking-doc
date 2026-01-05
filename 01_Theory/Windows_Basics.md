# Windows basics

## CMD
| Linux                 | Windows...                    |
|-----------------------|-------------------------------|
| `ls`                  | `dir`                         |
| `clear`               | `cls`                         |
| `mv` (for renaming)   | `ren`                         |
| `mv` (for moving)     | `move`                        |
| `rm`                  | `del`                         |
| `pwd`                 | `chdir`                       |
| `mkdir`               | `md`                          |
| `echo`                | `echo`                        |
| `cat`                 | `type`                        |
| `touch name`          | `copy nul name.txt`           |

## Concepts
- Regular executables (.exe) files are usually blocked.
    - Alternative types to use: WSH (.vbs), HTA (.hta), VBA, PSH
- Windows Scripting Host (WHS)
    - An administration tool that runs batch (windows equivalent to bash) files to automate tasks.
    - Execute VBScript: `wscript <file>` (must be a .vbs file)
    - .vbs files are usually blocked, hence: Execute .txt file as VBScript: `wscript /e:VBScript <file>`
- HTML Application (HTA)
- test

### Visual Basic Application
- Programming language to automate tasks in applications such as Word, Excel etc..
- Code snippets are called `macro`s and are there to automate certain tasks

#### Where to edit macros
- Word > empty document > View > Macros
    - Enter a name into the text box
    - At "Macros in:" select "Document1 (document)"
    - Click "create"

#### VBA Syntax
##### Variable declaration
```VBA
Dim payload As String
Dim num As Integer
Dim obj As Object
Dim tf As Boolean
```
- `Dim`: Keyword for variables
- `payload`: variable name
- `As String`: Datatype is string

##### Variable assignment
```VBA
payload = "calc.exe"
num = 42
```

##### Functions (Subroutines)
```VBA
Sub some_function()
    MsgBox("This will be displayed in a pop-up text box.")
End Sub
```

#### Example scripts
##### Automatically execute macro on opening of word file
```VBA
Sub some_function()
    MsgBox("This will be displayed in a pop-up text box.")
End Sub

Sub some_function()
    some_function
End Sub

Sub some_function()
    some_function
End Sub
```

##### Open the calculator
```VBA
Sub Calc()
    Dim payload As String
    payload = "calc.exe"
    CreateObject("Wscript.Shell").Run payload,0
```

- Important: File needs to be saved in "Macro-Enabled" format (`.doc` or `.docm`.
    - File > Save
    - "Save as type:": "Word 97-2003 Document"
    - Reopen: "SECURITY WARNING Macros have been disabled 'Enable Content'"
        - When clicking on 'Enable Content' the script get's executed
