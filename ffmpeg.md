# ffmpeg

## 得到影片時間長度

```bash
ffmpeg -i 30M.mp4 2>&1 | grep Duration | cut -d ' ' -f 4 | sed s/,//
```

```bash
# ffmpeg-python3
import ffmpeg
file = "30M.mp4"
print(ffmpeg.probe(file)['format']['duration'])

probe = ffmpeg.probe(file)
video_info = next((stream for stream in probe['streams'] if stream['codec_type'] == 'video'), None)
width = int(video_info['width'])
height = int(video_info['height'])
print(width, height)

# if want to get more
print(video_info)
```

## 轉檔\(解析度\)

透過 `scale` 來依照比例進行解析度轉換。  
備註：如果需要撲滿整個比例，需要加上 `setdar` 。  


```bash
ffmpeg -i in.mp4 -vf scale=320:240 out.mp4
ffmpeg -i in.mp4 -vf scale=320:240,setdar=4:3 out.mp4
```

## 



