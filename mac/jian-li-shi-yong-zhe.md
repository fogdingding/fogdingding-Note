# 建立使用者

```text
sudo dscl . -create /Users/fogdingding
sudo dscl . -create /Users/fogdingding UserShell /bin/bash
sudo dscl . -create /Users/fogdingding RealName "fogdingding"
sudo dscl . -create /Users/fogdingding UniqueID "66"
sudo dscl . -create /Users/fogdingding PrimaryGroupID 80
sudo dscl . -create /Users/fogdingding NFSHomeDirectory /Users/fogdingding
sudo dscl . -passwd /Users/fogdingding ji394c06
sudo dscl . -append /Groups/admin GroupMembership fogdingding
sudo mkdir /Users/fogdingding
sudo chown chown fogdingding:staff /Users/fogdingding
```

