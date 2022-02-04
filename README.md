<!-- # pytorch-video-understanding -->
# TAda! TAdaConv for Video Understanding

This repository provides the official pytorch implementation of the following papers for video classification and temporal localization. For more details on the respective paper, please refer to the [project folder](projects/). 

### Video/Action Classification

- **[TAda! Temporally-Adaptive Convolutions for Video Understanding](https://arxiv.org/pdf/2110.06178.pdf), ICLR 2022 [[Website](https://tadaconv-iclr2022.github.io)]**<br> 

- **[Towards Training Stronger Video Vision Transformers for EPIC-KITCHENS-100 Action Recognition](https://arxiv.org/pdf/2106.05058), CVPRW 2021**<br>
*Rank 2 submission to [EPIC-KITCHENS-100 Action Recognition challenge](https://competitions.codalab.org/competitions/25923#results)*

### Self-supervised video representation learning

- **[Self-supervised Motion Learning from Static Images](https://openaccess.thecvf.com/content/CVPR2021/papers/Huang_Self-Supervised_Motion_Learning_From_Static_Images_CVPR_2021_paper), CVPR 2021**<br>

- **[ParamCrop: Parametric Cubic Cropping for Video Contrastive Learning](https://arxiv.org/abs/2108.10501), arXiv 2021** (upcoming) <br>

### Temporal Action Localization

- **[A Stronger Baseline for Ego-Centric Action Detection](https://arxiv.org/pdf/2106.06942), CVPRW 2021**<br>
*Rank 1 submission to [EPIC-KITCHENS-100 Action Detection Challenge](https://competitions.codalab.org/competitions/25926#results)*

# About

This repository is released as part of the video understanding project [EssentialMC2](https://github.com/alibaba/EssentialMC2) from [DAMO Academy](https://damo.alibaba.com/?lang=en). [EssentialMC2](https://github.com/alibaba/EssentialMC2) provides industry-level solutions to video understanding problems, which includes representation learning, relation reasoning and openset life-long learning. 

# Latest

[2022-01] TAdaConv accepted to ICLR 2022.

[2021-10] Codes and models released.

# Guidelines

### Installation, data preparation and running

The general pipeline for using this repo is the installation, data preparation and running.
See [GUIDELINES.md](GUIDELINES.md).

### Using TAdaConv2d in your video backbone

To use TAdaConv2d in your video backbone, please follow the following steps:

```python
# 1. copy tada_branch somewhere in your project 
#    and import TAdaConv2d, RouteFuncMLP
from tada_branch import TAdaConv2d, RouteFuncMLP

# 2. define tadaconv and the route func in your model
def __init__(
self.conv_rf = RouteFuncMLP(
            c_in=64,            # number of input filters
            ratio=4,            # reduction ratio for MLP
            kernels=[3,3],      # list of temporal kernel sizes
)
self.conv = TAdaConv2d(
            in_channels     = 64,
            out_channels    = 64,
            kernel_size     = [1, 3, 3], # usually the temporal kernel size is fixed to be 1
            stride          = [1, 1, 1], # usually the temporal stride is fixed to be 1
            padding         = [0, 1, 1], # usually the temporal padding is fixed to be 0
            bias            = False,
            cal_dim         = "cin"
        )

# 3. replace 'x = self.conv(x)' with the following 
#    line in the self.forward(x) function
x = self.conv(x, self.conv_rf(x))
```

# Model Zoo

We include our pre-trained models in the [MODEL_ZOO.md](MODEL_ZOO.md).

# Feature Zoo

We include strong features for action localization on [HACS](http://hacs.csail.mit.edu/) and [Epic-Kitchens-100](https://epic-kitchens.github.io/2021) in our [FEATURE_ZOO.md](FEATURE_ZOO.md).

# Contributors

This codebase is written and maintained by [Ziyuan Huang](https://huang-ziyuan.github.io/), [Zhiwu Qing](https://scholar.google.com/citations?user=q9refl4AAAAJ&hl=zh-CN) and [Xiang Wang](https://scholar.google.com/citations?user=cQbXvkcAAAAJ&hl=zh-CN). 

## Citations
If you find our codebase useful, please consider citing the respective work :).
```BibTeX
@inproceedings{huang2021tada,
  title={TAda! Temporally-Adaptive Convolutions for Video Understanding},
  author={Huang, Ziyuan and Zhang, Shiwei and Pan, Liang and Qing, Zhiwu and Tang, Mingqian and Liu, Ziwei and Ang Jr, Marcelo H},
  booktitle={{ICLR}},
  year={2022}
}
```
```BibTeX
@inproceedings{mosi2021,
  title={Self-supervised motion learning from static images},
  author={Huang, Ziyuan and Zhang, Shiwei and Jiang, Jianwen and Tang, Mingqian and Jin, Rong and Ang, Marcelo H},
  booktitle={{CVPR}},
  pages={1276--1285},
  year={2021}
}
```
```BibTeX
@article{huang2021towards,
  title={Towards training stronger video vision transformers for epic-kitchens-100 action recognition},
  author={Huang, Ziyuan and Qing, Zhiwu and Wang, Xiang and Feng, Yutong and Zhang, Shiwei and Jiang, Jianwen and Xia, Zhurong and Tang, Mingqian and Sang, Nong and Ang Jr, Marcelo H},
  journal={arXiv preprint arXiv:2106.05058},
  year={2021}
}
```
```BibTeX
@article{qing2021stronger,
  title={A Stronger Baseline for Ego-Centric Action Detection},
  author={Qing, Zhiwu and Huang, Ziyuan and Wang, Xiang and Feng, Yutong and Zhang, Shiwei and Jiang, Jianwen and Tang, Mingqian and Gao, Changxin and Ang Jr, Marcelo H and Sang, Nong},
  journal={arXiv preprint arXiv:2106.06942},
  year={2021}
}
```