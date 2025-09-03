# GCC

Disable optimizations for a particular portion of the code:

```
#pragma GCC push_options
#pragma GCC optimize ("O0")

your code

#pragma GCC pop_options
```
