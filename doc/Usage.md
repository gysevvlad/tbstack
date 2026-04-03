# How to use

> Tested on u24

```
sudo ./tbstack --ptrace 2863482 | c++filt | less
```

It looks like the default scheme no longer works. No issues have been observed when using libunwind-ptrace.