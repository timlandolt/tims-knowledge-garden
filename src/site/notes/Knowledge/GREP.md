---
{"dg-publish":true,"permalink":"/knowledge/grep/","tags":["cli","grep"]}
---

---

**grep = Global Regular Expression Print**
Prints out lines matching a specific pattern

```bash
grep pattern file.txt

grep test file1.txt file2.txt # multiple files
grep -r test folder/path

grep test *.*
grep test **/*.*

grep test file.txt > output.txt

grep -i TeSt file.txt # case insensitive
grep -n test file.txt # prints line number along text
grep --color test file.txt # colors the search

grep ^start file.txt
grep end$ file.txt
```

