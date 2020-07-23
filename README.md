# MAL-inference
This repo is optimized for [Multiple Anchor Learning(MAL)](https://github.com/DeLightCMU/MAL) detector inference based on [NVIDIA Object Detection Toolkit (ODTK)](https://github.com/NVIDIA/retinanet-examples/).

For more details of MAL, please refer to our CVPR2020 paper: [Multiple Anchor Learning for Visual Object Detection](https://openaccess.thecvf.com/content_CVPR_2020/papers/Ke_Multiple_Anchor_Learning_for_Visual_Object_Detection_CVPR_2020_paper.pdf)  and the [original MAL repo](https://github.com/DeLightCMU/MAL).

## 1. Installation

### Requirements:
- Python>=3

### Step-by-step installation
```bash
# first, make sure that your conda is setup properly with the right environment
# for that, check that `which conda`, `which pip` and `which python` points to the
# right path. From a clean conda env, this is what you need to do
# conda activate

1.sudo docker run --gpus all -v /home/usrname/MAL-inference:/workspace --rm --ipc=host -it nvcr.io/nvidia/pytorch:19.10-py3
2 cd MAL-inference
3.python setup.py clean --all install
4.python setup.py build develop


## 2. Running for COCO metrics (Pytorch)
CUDA_VISIBLE_DEVICES=0 retinanet infer modelfold/modelname.pth --images ../coco/val2017/   --annotations ../coco/annotations/instances_val2017.json  --batch=1
note:
you need download cocco dataset in you computer

## 3. Running for single images (C++)
1.CUDA_VISIBLE_DEVICES=0 python retinanet/main.py export  --config_file configs/MAL_R-50-FPN_e2e.yaml  non.pth modelname.plan --size 800 1280(you can set high and wide according you need for example 800 1200 , 1024 1344 etc)
2.cp modelname.plan extras/cppapi/build
3. cd extras/cppapi/build
4. make -j8
5. ./infer modelname.plan picturename.png

## Citation: 

```bash
@inproceedings{kehuang2020,
  title={Multiple Anchor Learning for Visual Object Detection},
  author={Wei Ke and Tianliang Zhang and Zeyi Huang and Qixiang Ye and Jianzhuang Liu and Dong Huang},
  booktitle={CVPR},
  year={2020}
}
```
