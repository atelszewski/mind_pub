The Silver Searcher (ag)
========================

```
$ ag -C0 --nobreak --group --ignore ./build -s 'include.*stdio'

-C [LINES]
    Print lines before and after matches. Default is 2.

--nobreak
    Do not print a newline between matches in different files.

--group
    Group multiple matches in the same file together, and present
    them under a single occurrence of the filename.

--ignore PATTERN
    Ignore files/directories whose names match this pattern.
    Literal file and directory names are also allowed.

-G PATTERN
    Only search files whose names match PATTERN.

-i/-s/-S
    -i: Match case-insensitively.
    -s: Match case-sensitively.
    -S: Match case-sensitively if there are any uppercase letters in PATTERN,
        case-insensitively otherwise. Enabled by default.

-u
    Search all files. This ignores .ignore, .gitignore, etc.
    It searches binary and hidden files as well.

--depth NUM
    Search up to NUM directories deep, -1 for unlimited. Default is 25.
```
