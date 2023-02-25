## FF-GAN

This repository is the official code for the paper "Fine-grained Cross-modal Fusion based Refinement for Text-to-Image Synthesis" 

### Introduction

### How to use

0. **Requirements** 

```
Python >= 3.6
PyTorch >= 1.0
NVIDIA GPU + CUDA cuDNN
```

1. **Data** 
   1. Download metadata for [birds](https://drive.google.com/open?id=1O_LtUP9sch09QH3s_EBAgLEctBQ5JBSJ) [coco](https://drive.google.com/open?id=1rSnbIGNDGZeHlsUlLdahj0RJ9oo6lgH9) and save them to your path.
   2. Download the [birds](http://www.vision.caltech.edu/visipedia/CUB-200-2011.html) image data.
   3. Download [coco](http://cocodataset.org/#download) dataset.
   4. extract the source data to your path.

2. **Pretrained Models**
   1. the [models file](https://pan.baidu.com/s/1-V2Mp0wmX_tQxl6mOtnKpw) of our FF-GAN which obtain the best performance, this model obtain FID=14.56 on CUB-200 which is better than the result in our paper,CODE:zrE2.

3. Training 
   * Modify the parameters in parse to your local path
   * You can modify some parameters in the cfg file

```python
python /FF_GAN/code/main.py --cfg cfg/bird_DMGAN.yml --gpu 0
python /FF_GAN/code/main.py --cfg cfg/coco_DMGAN.yml --gpu 0
```


4. Validation

```python
# image genaration:
python /FF_GAN/code/main.py --cfg cfg/eval_bird.yml --gpu 0
python /FF_GAN/code/main.py --cfg cfg/eval_coco.yml --gpu 0

# FID
python fid_score.py --gpu 0 --batch-size 50 --path1 bird_val.npz --path2 your generated picture path
# R-precision
# You will get the result of R-precision when 30k pictures are generated
python /FF_GAN/code/main.py --cfg cfg/eval_bird.yml --gpu 0
python /FF_GAN/code/main.py --cfg cfg/eval_coco.yml --gpu 0

```
### Example results

* Images of different stages generated by our FF-GAN on CUB-200 and COCO datasets
![Figure_resolution](https://github.com/haoranhfut/FF-GAN/blob/main/code/fig/bird_resolution_box_final.png?raw=true)
* Qualitative results on CUB-200
![Figure_bird](https://github.com/haoranhfut/FF-GAN/blob/main/code/fig/figure_bird_coco.png?raw=true)
* Qualitative results on COCO
![Figure_coco](https://github.com/haoranhfut/FF-GAN/blob/main/code/fig/figure_coco_box.png?raw=true)
* Attention visualization on CUB-200 test sets
![Atten](https://github.com/haoranhfut/FF-GAN/blob/main/code/fig/attention_map.png?raw=true)


### Acknowlegement
The pre-process data and code borrows heavily from [Attn-GAN](https://github.com/taoxugit/AttnGAN) and [DM-GAN](https://github.com/MinfengZhu/DM-GAN), we apprecite the authors for sharing their codes and data.
