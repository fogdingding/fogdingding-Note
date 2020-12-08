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
sudo dd if=Downloads/SW_DVD9_Win_Pro_10_1909_64BIT_ChnTrad_Pro_Ent_EDU_N_MLF_X22-17389.ISO of=/dev/disk2 bs=1m
```

