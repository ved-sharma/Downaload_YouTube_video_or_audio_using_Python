We will work with the Anaconda distribution of Python, and use the [pytube](https://pytube.io/en/latest/index.html) package to download YouTube videos (mp4) or audio only files (mp3)

1. Open Anaconda prompt and create a new environment (called YT) with python 3.8  
  <code>> conda create -n YT python=3.8</code>  

2. Activate the environemnt: <code>> conda activate YT</code>   

3. Once in the environment, install pytube and jupyter  
<code>> pip install pytube</code>   
<code>> conda install jupyter</code>   

4. Launch <code>> jupyter lab</code>, which will open a notebook in the default browser. Enter following code:  

```python
# import packages
from pytube import YouTube
import os

# Put the YouTube url to download
yt = YouTube("https://www.youtube.com/watch?v=Dzej2YDQM6Q") 
```
## To save video+audio as an .mp4 file
Each YouTube video is available as multiple versions (called streams) with different video quality (resolution) and whether it contains both the video+audio or just the video or audio.

```python
# Filter for progressive streams, which have both the video and audio in one file
print(*yt.streams.filter(progressive=True), sep='\n') 
```
We filter for [Progressive streams](https://pytube.io/en/latest/user/streams.html#filtering-streams), which contain both the video and audio in a single file. Here are the results of running the above line. Three different streams (3gpp and mp4 videos with 144p, 360p and 720p resolutions) are found, each one identified with a specific itag number.

<Stream: itag="17" mime_type="video/3gpp" res="144p" fps="6fps" vcodec="mp4v.20.3" acodec="mp4a.40.2" progressive="True" type="video">  
<Stream: itag="18" mime_type="video/mp4" res="360p" fps="25fps" vcodec="avc1.42001E" acodec="mp4a.40.2" progressive="True" type="video">  
<Stream: itag="22" mime_type="video/mp4" res="720p" fps="25fps" vcodec="avc1.64001F" acodec="mp4a.40.2" progressive="True" type="video">  

```python
# get stream 18, which is a mp4 video with 360p resolution
video = yt.streams.get_by_itag(18)

# check for destination to save file
print("Enter the destination (leave blank for current directory)")
destination = str(input(">> ")) or '.'
  
# download the file as an mp4 file
out_file = video.download(output_path=destination)
  
# result of success
print(yt.title + " has been successfully downloaded.")
```
## To save only the audio .mp3 file
```python
# filter strems for audio only files
print(*yt.streams.filter(only_audio=True), sep='\n')
```
<Stream: itag="139" mime_type="audio/mp4" abr="48kbps" acodec="mp4a.40.5" progressive="False" type="audio">  
<Stream: itag="140" mime_type="audio/mp4" abr="128kbps" acodec="mp4a.40.2" progressive="False" type="audio">  
<Stream: itag="251" mime_type="audio/webm" abr="160kbps" acodec="opus" progressive="False" type="audio">  

We see that there are three audio streams available. We'll downaload the first one.
```python
# get the first audio stream
video = yt.streams.filter(only_audio=True).first()

# destination for the audio file
print("Enter the destination (leave blank for current directory)")
destination = str(input(">> ")) or '.'
  
# download the file. Filename needs to be defined explicitly as an mp3, otherwise it will download the audio file as an mp4
out_file = video.download(output_path=destination, filename=yt.title+".mp3")
  
# result of success
print(yt.title + " has been successfully downloaded.")
```

## Link to the Jupyter notebook
[Download YT video or audio](https://github.com/ved-sharma/Downaload_YouTube_video_audio/blob/224006cc88fc10210362c7e3c349ec497c9f2a2d/Download%20YT%20video%20or%20audio.ipynb)

## Credit  
https://www.geeksforgeeks.org/download-video-in-mp3-format-using-pytube/
