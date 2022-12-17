## Multi-resolution Monocular Depth Map Fusion by Self-supervised Gradient-based Composition

This repository contains code and models for our [paper](https://arxiv.org/pdf/2212.01538.pdf):

> [1] Yaqiao Dai, Renjiao Yi, Chenyang Zhu, Hongjun He, Kai Xu,  Multi-resolution Monocular Depth Map Fusion by Self-supervised  Gradient-based Composition, AAAI 2023

![](./figures/1.gif)

![](./figures/2.gif)

![](./figures/3.gif)

### Changelog 

* [November 2022] Initial release of code and models

### Setup 

1) Download the code.
```shell
 git clone https://github.com/YuiNsky/Gradient-based-depth-map-fusion.git
 cd Gradient-based-depth-map-fusion
```




2. Set up dependencies: 
    2.1  Create conda virtual environment.
    
    ```shell
    conda env create -f GBDF.yaml
    conda activate GBDF
    ```
    
    2.2  Install pytorch in virtual environment.
    ```shell
    pip install torch==1.9.1+cu111 torchvision==0.10.1+cu111 torchaudio==0.9.1 -f https://download.pytorch.org/whl/torch_stable.html
    ```



3. Create a folder `models` Download fusion model [model_dict.pt](https://github.com/1kaiser/Gradient-based-depth-map-fusion/releases/download/v0.1/model_dict.pt) and place in the folder `models`.

   


4. Download one or more backbone pretrained model.

     ​     LeRes: [res50.pth](https://github.com/1kaiser/Gradient-based-depth-map-fusion/releases/download/v0.1/res50.pth) or [res101.pth](https://github.com/1kaiser/Gradient-based-depth-map-fusion/releases/download/v0.1/res101.pth), place in the folder `LeRes`.

   ​     MiDas: [model.pt](https://github.com/1kaiser/Gradient-based-depth-map-fusion/releases/download/v0.1/model.pt), place in the folder `MiDaS`.
    


5. The code was tested with Python 3.8, PyTorch 1.9.1, OpenCV 4.6.0.

### Usage 

1) Place one or more input images in the folder `input`.

2) Run our model with a monocular depth estimation method:

    ```shell
    python run.py -p LeRes50
	```


3) The results are written to the folder `output`, every result is the combination of input image, backbone prediction and our prediction.

​		Use the flag `-p` to switch between different backbones. Possible options are `LeRes50` (default), `LeRes101`, `SGR`, `MiDaS`, `DPT` and `NeWCRFs`.

### Evaluation

Our evaluation contains three published high resolution datasets, which are Multiscopic, Middleburry2021 and Hypersim. 

To evaluate our model on Multiscopic, you can download this dataset [here](https://sites.google.com/view/multiscopic). You need to download the test dataset, rename it as `multiscopic` and place it in folder `datasets`.

To evaluate our model on Middleburry2021, you can download this dataset [here](https://vision.middlebury.edu/stereo/data/scenes2021/zip/all.zip). You need to unzip the dataset, rename it as `2021mobile`  and place it in folder `datasets`.

To evaluate our model on Hypersim, you can download the whole dataset [here](https://github.com/apple/ml-hypersim/blob/main/code/python/tools/dataset_download_images.py). We also provide the evaluation subsets [hypersim](https://shanghaitecheducn-my.sharepoint.com/:u:/g/personal/chenky12022_shanghaitech_edu_cn/EZcASVNppkNIo34mSBiXUjAByGyg4HCEXW0voRdnmT-sQg?e=1opopk). You need to download the subsets and place it in folder `datasets`.



Then you can evaluate our fusion model with specified monocular depth estimation method and dataset:

```shell
python eval.py -p LeRes50 -d middleburry2021
```

Use the flag `-p` to switch between different backbones. Possible options are `LeRes50` (default),  `MiDaS`

Use the flag `-d` to switch between different datasets. Possible options are `middleburry2021` (default), `multiscopic` and `hypersim`.

### Training

Our model was trained based on backbone LeRes and dataset HR-WSI, we use guided filter to preprocess the dataset and select high quality results as our training datasets based on canny edge detection. You need to download the preprocessed dataset [HR](https://shanghaitecheducn-my.sharepoint.com/:u:/g/personal/chenky12022_shanghaitech_edu_cn/EQWICYjodhFCjiimYsLSUDABI5-sYddf6MleupjU0RRPWQ?e=GahsRB) and place it in the folder `datasets`.

Then you can train our fusion model using GPU:

```shell
python train.py
```


### Citation

Please cite our papers if you use this code. 
```
@article{dai2022multi,
  title={Multi-resolution Monocular Depth Map Fusion by Self-supervised Gradient-based Composition},
  author={Dai, Yaqiao and Yi, Renjiao and Zhu, Chenyang and He, Hongjun and Xu, Kai},
  journal={arXiv preprint arXiv:2212.01538},
  year={2022}
}
```

### License 

MIT License 
