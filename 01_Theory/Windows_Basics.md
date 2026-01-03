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
- Windows Scripting Host (WHS): administration tool that runs batch (windows equivalent to bash) files to automate tasks.
- Execute VBScript: `wscript <file>` (must be a .vbs file)
- Execute .txt file as VBScript: `wscript /e:VBScript <file>`
