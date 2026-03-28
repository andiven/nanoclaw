---
name: video-editor
description: Video and audio processing skill using ffmpeg-python and moviepy. Use this for cutting, merging, or adding text to videos.
---

# Video Editing Skill

This skill allows you to programmatically edit videos and audio using `moviepy` (which wraps `ffmpeg`).

## Dependencies
Ensure these are installed:
```bash
pip install moviepy
```
*(Requires system-level `ffmpeg` to be installed, which is usually handled in the Dockerfile)*

## Common Operations

### 1. Cut a Video (Extract a subclip)
```python
from moviepy.editor import VideoFileClip

# Extract from 10s to 20s
clip = VideoFileClip("input.mp4").subclip(10, 20)
clip.write_videofile("cut_output.mp4", codec="libx264")
clip.close()
```

### 2. Merge Multiple Videos
```python
from moviepy.editor import VideoFileClip, concatenate_videoclips

clip1 = VideoFileClip("video1.mp4")
clip2 = VideoFileClip("video2.mp4")

final_clip = concatenate_videoclips([clip1, clip2])
final_clip.write_videofile("merged.mp4", codec="libx264")

clip1.close()
clip2.close()
final_clip.close()
```

### 3. Add Audio to Video
```python
from moviepy.editor import VideoFileClip, AudioFileClip

video = VideoFileClip("video_no_audio.mp4")
audio = AudioFileClip("background_music.mp3")

# Set audio to video (and cut audio if it's longer than video)
final_video = video.set_audio(audio.subclip(0, video.duration))
final_video.write_videofile("video_with_audio.mp4", codec="libx264", audio_codec="aac")

video.close()
audio.close()
```

## Best Practices
1. **Always close clips**: `moviepy` can leave file handles open. Always call `.close()` on your clips when done.
2. **Specify codecs**: Always use `codec="libx264"` for video and `audio_codec="aac"` for audio to ensure broad compatibility (especially for web/social media).
3. **Memory management**: Video processing is RAM intensive. Avoid loading massive videos entirely into memory if possible.
