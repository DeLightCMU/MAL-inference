# MAL-inference
This repo is optimized for [Multiple Anchor Learning(MAL)](https://github.com/DeLightCMU/MAL) detector inference based on [NVIDIA Object Detection Toolkit (ODTK)](https://github.com/NVIDIA/retinanet-examples/).

For more details of MAL, please refer to our CVPR2020 paper: [Multiple Anchor Learning for Visual Object Detection](https://openaccess.thecvf.com/content_CVPR_2020/papers/Ke_Multiple_Anchor_Learning_for_Visual_Object_Detection_CVPR_2020_paper.pdf)  and the [original MAL repo](https://github.com/DeLightCMU/MAL).

## 1. Installation

### Requirements:
- Python>=3

### Step-by-step installation
```bash
# install MAL-inference
git https://github.com/DeLightCMU/MAL-inference.git

# load MAL-inference in NVIDIA docker
sudo docker run --gpus all -v /home/usrname/MAL-inference:/workspace --rm --ipc=host -it nvcr.io/nvidia/pytorch:19.10-py3

# the following will install the lib with
# symbolic links, so that you can modify
# the files if you want and won't need to
# re-build it
cd MAL-inference
python setup.py clean --all install
python setup.py build develop
#re-build C++ code
cd extras/cppapi/build
rm -rf *
cmake -DCMAKE_CUDA_FLAGS="--expt-extended-lambda -std=c++11" ..
make -j8
```

## 2. Running for COCO metrics (Pytorch)
```bash
CUDA_VISIBLE_DEVICES=0 retinanet infer "path to config file.yaml" MODEL.WEIGHT "path to.pth file" --images "path to coco dataset/val2017/"   --annotations "path to coco dataset/annotations/instances_val2017.json"  --batch=1

note:
you need download cocco dataset in you computer  [COCO 2017](http://cocodataset.org/#download)
```
## 3. Running for single images (C++)
```bash
#export model to Tensorrt format 
CUDA_VISIBLE_DEVICES=0 python retinanet/main.py export  --"path/to/config/file.yaml"  non.pth modelname.plan --size 800 1280(you can set high and wide according you need for example 800 1200 , 1024 1344 etc)

cp modelname.plan extras/cppapi/build

cd extras/cppapi/build

./infer modelname.plan picturename.png
```
## Citation: 

```bash
@inproceedings{kehuang2020,
  title={Multiple Anchor Learning for Visual Object Detection},
  author={Wei Ke and Tianliang Zhang and Zeyi Huang and Qixiang Ye and Jianzhuang Liu and Dong Huang},
  booktitle={CVPR},
  year={2020}
}
```
