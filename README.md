# Simple-SR
The repository includes MuCAN, LAPAR, Beby-GAN and etc. It is designed for simple training and evaluation.

---
### Update
The training code of LAPAR (9 models) is now released.

---
### Paper 

#### Best-Buddy GANs for Highly Detailed Image Super-Resolution
[\[High quality version\]](https://drive.google.com/file/d/14vt57mSERR8cx62e7aNCkuxlKOCUP53H/view?usp=sharing)

#### MuCAN: Multi-Correspondence Aggregation Network for Video Super-Resolution (ECCV 2020)
[\[ECCV\]](https://www.ecva.net/papers/eccv_2020/papers_ECCV/papers/123550341.pdf)   [\[arXiv\]](https://arxiv.org/abs/2007.1180)

#### LAPAR: Linearly-Assembled Pixel-Adaptive Regression Network for Single Image Super-resolution and Beyond (NeurIPS 2020)
[\[NeurIPS\]](https://papers.nips.cc/paper/2020/file/eaae339c4d89fc102edd9dbdb6a28915-Paper.pdf)

Please find supplementary files of MuCAN and LAPAR [here](https://drive.google.com/drive/folders/1pSFX6kV81slv2vGkboZjewZwQsLkFesU).

---
### Usage

1. Clone the repository
    ```shell
    git clone https://github.com/Jia-Research-Lab/Simple-SR.git
    ```
2. Install the dependencies
    - Python >= 3.5
    - PyTorch >= 1.2
    - spatial-correlation-sampler
    ```shell
    pip install spatial-correlation-sampler
    ```
    - Other packages
    ```shell
    pip install -r requirements.txt
    ```

3. Download pretrained models from [Google Drive](https://drive.google.com/drive/folders/1c-KUEPJl7pHs9btqHYoUJkcMPKViObgJ?usp=sharing). We re-trained the LAPAR models and their results are slightly different from the ones reported in paper.
    - MuCAN
        - MuCAN\_REDS.pth: trained on REDS dataset, 5-frame input, x4 scale
        - MuCAN\_Vimeo90K.pth: trained on Vimeo90K dataset, 7-frame input, x4 scale
    - LAPAR: trained on DIV2K+Flickr2K datasets
        |    Scale x2    |    Scale x3    |    Scale x4    |
        |     :----:     |     :----:     |     :----:     |
        | LAPAR_A_x2.pth | LAPAR_A_x3.pth | LAPAR_A_x4.pth |
        | LAPAR_B_x2.pth | LAPAR_B_x3.pth | LAPAR_B_x4.pth |
        | LAPAR_C_x2.pth | LAPAR_C_x3.pth | LAPAR_C_x4.pth |

4. Quick test
    ```shell
    python3 test_sample.py --sr_type SISR/VSR --model_path /model/path --input_path ./demo/LR_imgs --output_path ./demo/output --gt_path ./demo/HR_imgs
    ```

#### Data Preparation
1. Training Datasets

Download [DIV2K](https://data.vision.ee.ethz.ch/cvl/DIV2K/) and [Flickr2K](https://cv.snu.ac.kr/research/EDSR/Flickr2K.tar). You can crop the HR and LR images to sub-images for fast reading referring to .utils/data\_prep/extract\_subimage.py. 

2. Evaluation Datasets

Download Set5, Set14, Urban100, BSDS100 and Manga109 from [Google Drive](https://drive.google.com/drive/folders/1B3DJGQKB6eNdwuQIhdskA64qUuVKLZ9u) uplaoded by BasicSR.

3. Update the dataset location in .dataset/\_\_init\_\_.py. 

4. (Optional) You can convert images to lmdb files for fast loading referring to [BasicSR](https://github.com/xinntao/BasicSR/blob/master/docs/DatasetPreparation.md#LMDB-Description). And you need to modify the data reading logics in .dataset/\*dataset.py accordingly.

#### Train
1. Create a log folder as
    ```shell
    mkdir logs
    ```

2. Create a new experiment folder in .exps/. You just need to prepare the config.py and network.py, while the train.py and validate.py are universal. For example, for LAPAR\_A\_x2, run
    ```shell
    cd exps/LAPAR_A_x2/
    bash train.sh $GPU_NUM $PORT
    ```
Notice that you can find the checkpoints, log files and visualization images in either .exps/LAPAR\_A\_x2/log/ (a soft link) or .logs/LAPAR\_A\_x2/.

#### Test
Please refer to validate.py in each experiment folder or quick test above.

---
### Acknowledgement
We refer to [BasicSR](https://github.com/xinntao/BasicSR) for some details.

---
### Bibtex
    @inproceedings{li2020mucan,
      title={MuCAN: Multi-correspondence Aggregation Network for Video Super-Resolution},
      author={Li, Wenbo and Tao, Xin and Guo, Taian and Qi, Lu and Lu, Jiangbo and Jia, Jiaya},
      booktitle={European Conference on Computer Vision},
      pages={335--351},
      year={2020},
      organization={Springer}
    }
    @article{li2020mucan,
      title={MuCAN: Multi-Correspondence Aggregation Network for Video Super-Resolution},
      author={Li, Wenbo and Tao, Xin and Guo, Taian and Qi, Lu and Lu, Jiangbo and Jia, Jiaya},
      journal={arXiv preprint arXiv:2007.11803},
      year={2020}
    }
    @article{li2021best,
      title={Best-Buddy GANs for Highly Detailed Image Super-Resolution},
      author={Li, Wenbo and Zhou, Kun and Qi, Lu and Lu, Liying and Jiang, Nianjuan and Lu, Jiangbo and Jia, Jiaya},
      journal={arXiv preprint arXiv:2103.15295},
      year={2021}
    }
