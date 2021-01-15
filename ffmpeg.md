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

## 



