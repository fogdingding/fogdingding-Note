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
video = next((stream for stream in probe['streams'] if stream['codec_type'] == 'video'), None)
width = int(video['width'])
height = int(video['height'])
print(width, height)
```

## 



