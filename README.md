We will work using conda installation.  
Open Anaconda prompt and create a new environment with python 3.8  
  <code>> conda create -n YT python=3.8</code>  
activate the environemnt: <code>> conda activate YT</code>   
Once in the environment, install pytube and jupyter  
<code>> pip install pytube</code>   
<code>> conda install jupyter</code>   
Launch <code>> jupyter lab</code>  
```python
# importing packages
from pytube import YouTube
import os
```
