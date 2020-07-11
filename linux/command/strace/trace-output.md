# trace output option

`strace -o filename command`

で、commandのシステムコールをトレースすることができる。

## 例

`strace -o log.txt sleep 1`

log.txtに、呼び出したシステムコールの内容が出力される。

```
openat(AT_FDCWD, "/usr/lib/locale/C.UTF-8/LC_CTYPE", O_RDONLY|O_CLOEXEC) = 3
fstat(3, {st_mode=S_IFREG|0644, st_size=201272, ...}) = 0
mmap(NULL, 201272, PROT_READ, MAP_PRIVATE, 3, 0) = 0x7fd1e507e000
close(3)                                = 0
clock_nanosleep(CLOCK_REALTIME, 0, {tv_sec=1, tv_nsec=0}, NULL) = 0
```

# 参考

https://youtu.be/kF1VicngujU 
