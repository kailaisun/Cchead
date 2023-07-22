# cchead


Code for paper: Toward Pedestrian Head Tracking: A Benchmark Dataset and an Information Fusion Network


Dataset Download: https://cloud.tsinghua.edu.cn/d/a9f2703b83a54dc7b569/
Video Demo: https://drive.google.com/drive/folders/1BLmzCRx3MbOzVUITw0-RCpRqTHJ2JXYQ?usp=sharing

## Environment
- The code is tested on Ubuntu 20.04.2, python 3.8, cuda 11.1.


## Installation
 1. Install pytorch

  ```bash
  pip install torch==1.8.0+cu111 torchvision==0.9.0+cu111 torchaudio==0.8.0 -f https://download.pytorch.org/whl/torch_stable.html
  ```

 2. Clone this repository
  ```bash
  git clone https://github.com/kailaisun/FFO
  ```
  
 3. Install 
  ```bash
  pip install -r requirements.txt
  ```
  
## Train
```Bash
python people_detect.py --path <video_path>
```

## Test

```Bash
python people_detect.py --path <video_path>
```
- Result of SCM

- You can modify hyperparameters of JointDet module in person_detect.py.
```python 
 result_info = joint_de(head_info, other_info,thresh=0.8,conf=0.6,thresh1=0.8)  #line 50
```
