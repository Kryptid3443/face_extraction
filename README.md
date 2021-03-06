# face extraction

Installed on `pia` inside `/userdata/bdichter/envs/py35`

## Installation
I recommend using a conda envoronment.
`ffmpeg` and `dlib` are required. If on mac, install `ffmpeg` by running `brew install ffmpeg`. 
Installing `dlib` on a mac is a bit of an ordeal. [This post](http://www.pyimagesearch.com/2017/03/27/how-to-install-dlib/) should help. It also uses `opencv3`, however I was only able to get this to work in python 3.5, so I used conda 
virtual environment. Putting it all together (assuming anaconda is properly
installed):
```bash
brew install ffmpeg
conda create -n face_extraction_env python=3.5 pillow numpy
source activate face_extraction_env
conda install -c menpo opencv3
pip install tqdm
pip install face_recognition
```
## Usage
```python
from face_extraction import detect_faces_video
detect_faces_video('video_in.mp4', 'video_out.avi')
```

OpenCV is pretty picky about the form of the input video, so you may 
have to use `ffmpeg` to change the video codec. I have had the most luck with
.mp4 files with an mpeg4 vcodec. The recording setup uses h256, which doesn't
work right away. Here is an example convertion:
```
ffmpeg -i SN6.mp4 -vcodec mpeg4 SN6_v2.mp4
```

## Ideas
* Implement in C++
* split video up with ffmpeg, run on different cores, then recombine them
