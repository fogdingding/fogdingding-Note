# DD 燒入



```csharp
# 查看目前硬碟有哪些
diskutil list
```

```bash
# 卸載
diskutil unmountDisk /dev/disk2
```

```bash
# 燒入
sudo dd if=xxxx.ISO of=/dev/disk2 bs=1m
```



