---
description: 輸入一些指令後，按下方向鍵上或方向鍵下，即可回朔相關指令。
---

# 快捷鍵-歷史查詢

編輯設定檔案

```text
vim ~/.bashrc
```

加入以下指令

```text
bind '"\x1b\x5b\x41":history-search-backward'
bind '"\x1b\x5b\x42":history-search-forward'
```

重啟設定檔案

```text
source ~/.bashrc
```

