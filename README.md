# BEDSR-Net

This repository is unofficial implementation of [BEDSR-Net: A Deep Shadow Removal Network From a Single Document Image](https://openaccess.thecvf.com/content_CVPR_2020/html/Lin_BEDSR-Net_A_Deep_Shadow_Removal_Network_From_a_Single_Document_CVPR_2020_paper.html) [Lin+, CVPR 2020] with PyTorch.

A refined version of [IsHYuhi's implementation](https://github.com/IsHYuhi/BEDSR-Net_A_Deep_Shadow_Removal_Network_from_a_Single_Document_Image).

## Fix several problems
1. nn.ConvTranspose2d compatible with higher version of Pytorch
2. gradcam uses too much vram, use [pytorch-grad-cam](https://github.com/jacobgil/pytorch-grad-cam) instead
3. provide default correct training config
4. provide easy inference code

## Dependencies
Pytorch, torchvision, matplotlib, wandb, albumentations, pytorch-grad-cam

## Dataset Structure

The dataset should be formatted like below, train.csv and test.csv can be generated.
You can download the Jung dataset: [csv](https://drive.google.com/file/d/1NS4cxMwoGrWlHv6uyf8iVFAUN-xmw5vb/view?usp=sharing)/[images](https://drive.google.com/file/d/192dqE4K6zuxD0tNre9UHDwu4YB4uxSnG/view?usp=sharing).

```
.
├── csv/
│   └── Jung/
│       ├── train.csv
│       └── test.csv
└── dataset/
    └── Jung/
        ├── train/
        │   ├── input/
        │   │   ├── *.jpg
        │   │   └── ...
        │   └── target/
        │       ├── *.jpg
        │       └── ...
        └── test/
            ├── input/
            │   ├── *.jpg
            │   └── ...
            └── target/
                ├── *.jpg
                └── ...
```


## Training

1. Training BE-Net
```bash
$ python train_benet.py --config ./configs/model\=benet/config.yaml
```

2. Training BEDSR-Net
```bash
$ python train_bedsrnet.py --config ./configs/model\=bedsrnet/config.yaml
```

You can use [W&B](https://wandb.ai/site) by `--use_wandb`.

## Infer

mask sure put all your model state_dict into pretrained directory

```bash
$ python infer.py
```

result images will be produced in results folder
