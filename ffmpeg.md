# ffmpeg

## 得到影片時間長度

```bash
ffmpeg -i 30M.mp4 2>&1 | grep Duration | cut -d ' ' -f 4 | sed s/,//
```



