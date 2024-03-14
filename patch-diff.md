# Diff, patch

### Diff format explained

The `-u` option you used specifies the unified format.
In that format the first two lines is a header:

```
--- is the original file,
+++ is the new file, and the timestamps.
```

```
@@ block headers
```

That is then followed by chunks (change hunks) that starts with
the `@@ -R,r +R,r @@` syntax.

Those are two ranges, the one with the `-` is the range for the chunk in the original
file, and the one with the `+` the range in the new file. The `R` designates
the line number where the diff operation is started.

The numbers after the comma are the number of affected lines in each file.

- Every time you _remove_ a line, the `+r` number will be smaller than `-r`.
- Every time you _add_ a line, the `+r` number will be bigger than `-r`.
- Changing a line will add `0` to the `+r` number (same scope of lines).

**Chunks of code lines**

Within these chunks lines are identified as additions or deletions `-` means delete,
`+` means addition. Lines that did not change in that chunk will have neither `+` nor
`-` front of it.
