# cchead


Code for paper: Toward Pedestrian Head Tracking: A Benchmark Dataset and an Information Fusion Network


Dataset Download: https://cloud.tsinghua.edu.cn/d/a9f2703b83a54dc7b569/


Video Demo: https://drive.google.com/drive/folders/1BLmzCRx3MbOzVUITw0-RCpRqTHJ2JXYQ?usp=sharing

We uploaded both raw videos and filefolder of images and labels. If you want to replicate our experiment, you should unzip the 4 zipfiles into <yourpathtopaddledet/dataset/mot/>.

This filefolder contains what we directly applied in our methods.

It form the dataset as:

--balanced_data
       --images
          --train
             --90T_25fps
                --img
                    --0.jpg
                    --1.jpg
                    ......
                --seqinfo.ini
             ......

         --test
            --90cross_25fps
               --img
                  --0.txt
                  --1.txt
                --gt
                   --gt.txt
                --seqinfo.ini
             ......


      --labels_with_ids
         --train
            --90T_25fps
               --img
                  --0.txt
                  --1.txt
                  ......

         --test
            --90cross_25fps
               --img
                  --0.txt
                  --1.txt
                  ......

where gt.txt is used for evaluation, it is formed as:
1,1,57,86,28,32,1,1,1  (frame_id, track_id, xy (left&up) wh,...)
2,1,55,87,28,32,1,1,1
3,1,60,85,28,32,1,1,1
4,1,63,85,29,31,1,1,1
5,1,64,85,29,31,1,1,1
6,1,66,83,29,31,1,1,1
...
1,2,65,146,50,56,1,1,1 (frame_id, track_id, xy (left&up) wh,...)

label files for training such as 0.txt is formed as:
0 186 0.23671875 0.25069444444444444 0.0067708333333333336 0.015277777777777777 (class_ind, track_id, xy (center) wh)
.......
xywhs in label files are all scaled to (0,1)

seqinfo.ini contains the following information:

[Sequence]
name=90T_25fps
imDir=img
frameRate=25
seqLength=1110
imWidth=1920
imHeight=1080
imExt=.jpg

If you are using paddledetection, you may modify codes of loading data to train network on this dataset.

## Environment
- The code is tested on Ubuntu 20.04.2, python 3.9, cuda 11.7，Paddle 2.4.2, PaddleDet 2.6.


## Installation

Please refer to [Installation]((https://github.com/PaddlePaddle/PaddleDetection/blob/release/2.6/docs/tutorials/INSTALL_cn.md) for installation instructions of Paddle and PaddleDet.

We modified some codes in PaddleDet, please clone them and replace the original code in PaddleDet.
  
## Train
```Bash
python -m paddle.distributed.launch --log_dir=./fairmot_dla34_40e_1088x608_mifn/ --gpus 0,1,2,3 tools/train.py -c configs/mot/fairmot/fairmot_ourdata_dla34_40e_1088x608_mifn.yml```

## Test

```Bash
CUDA_VISIBLE_DEVICES=1 python tools/eval_mot.py -c configs/mot/fairmot/fairmot_ourdata_dla34_40e_1088x608_mifn.yml -o weights=output/fairmot_ourdata_dla34_40e_1088x608_mifn/model_final.pdparams
```


## Acknowledgement
MMDetection is an open source project that is contributed by researchers and engineers from various colleges and companies. We appreciate all the contributors who implement their methods or add new features, as well as users who give valuable feedbacks. We wish that the toolbox and benchmark could serve the growing research community by providing a flexible toolkit to reimplement existing methods and develop their own new detectors.
