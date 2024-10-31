# Casual-Story
CAUSAL-STORY: Local Causual Attention Utilizing Parameter-Efficient Tuning For Visual Story Synthesis

# Introduction
The excellent text-to-image synthesis capability of diffusion models has driven progress in synthesizing coherent visual stories. The current state-of-the-art method combines the features of historical captions, historical frames, and the current captions as conditions for generating the current frame. However, this method treats each historical frame and caption as the same contribution. It connects them in order with equal weights, ignoring that not all historical conditions are associated with the generation of the current frame. To address this issue, we propose Causal-Story. This model incorporates a local causal attention mechanism that considers the causal relationship between previous captions, frames, and current captions. By assigning weights based on this relationship, Causal-Story generates the current frame, thereby improving the global consistency of story generation. We evaluated our model on the PororoSV and FlintstonesSV datasets and obtained state-of-the-art FID scores, and the generated frames also demonstrate better storytelling in visuals.


Here are the example of two tasks this work focus on:
![GitHub Logo](https://github.com/styufo/Causal-Story/blob/main/example.png)

Code for (["CAUSAL-STORY: Local Causual Attention Utilizing Parameter-Efficient Tuning For Visual Story Synthesis (ICASSP 2024)"](https://ieeexplore.ieee.org/abstract/document/10446420)).


# Architecture
![GitHub Logo](https://github.com/styufo/Causal-Story/blob/main/arti.png)
Model architecture of Causal-Story. Our model is inspired by ([ARLDM](https://openaccess.thecvf.com/content/WACV2024/html/Pan_Synthesizing_Coherent_Story_With_Auto-Regressive_Latent_Diffusion_Models_WACV_2024_paper.html)). The solid line box represents the overall structure of the denoising U-Net section of stable diffusion model, while the dashed line box introduces the specific composition of key modules. The green dashed box displays the location of the local causal attention module and adapter, while the gray dashed box displays the details of the local causal attention module.

# Setup your Environment
First, you need to create a corresponding conda environment：
```python
conda create -n Causal-Story python=3.8
conda activate Causal-Story
conda install pytorch torchvision torchaudio cudatoolkit=10.2 -c pytorch-lts
git clone https://github.com/styufo/Causal-Story.git
cd Causal-Story
pip install -r requirements.txt
```

# Data Preparation
*The FlintstonesSV Dataset can be downloaded from here(["google drive"](https://drive.usercontent.google.com/download?id=1kG4esNwabJQPWqadSDaugrlF4dRaV33_&export=download&authuser=0))or["百度云盘（提取码jufe）"](https://pan.baidu.com/s/18JzrFpEqj30QnoLmgSHx5w?pwd=jufe).


*The Pororo Dataset can be downloaded from here(["google drive"](https://drive.usercontent.google.com/download?id=11Io1_BufAayJ1BpdxxV2uJUvCcirbrNc&export=download&authuser=0)) or["百度云盘（提取码5cy8）"](https://pan.baidu.com/s/1sreh7FY4sNJAWeubCCR1oA?pwd=5cy8).


To accelerate I/O, using the following scrips to convert your downloaded data to HDF5:


Tips: The path of "data_dir" and "save_path" can be set according to your actual situation.
```python
python data_script/pororo_hdf5.py
--data_dir /path/to/pororo_data
--save_path /path/to/save_hdf5_file

python data_script/flintstones_hdf5.py
--data_dir /path/to/flintstones_data
--save_path /path/to/save_hdf5_file
```


we also provide the hdf5 files here for directly use (but the files are honestly large):


FlintstonesSV hdf5:["百度云盘（提取码3853）"](https://pan.baidu.com/s/1LcbNoMKqP2nF9RHUFUQYzw?pwd=3853).


Pororo hdf5: ["百度云盘（提取码39g9）"](https://pan.baidu.com/s/1Mxn2fWhbC7RJsq8W4EmVDA?pwd=39g9).


# Training
You need to modify the parameters in config. yaml according to the location of your file. And than, run:
```python
python main.py
```


# Sample
Modify the parameters in config. yaml according to the location of your file and change from 'train' to 'sample' and than, run:
```python
python main.py
```


# Acknowledgment
Thanks a lot to @xichenpan for kindly sharing the code of AR-LDM.


# Citation
If you find this code useful for your research, please cite our paper:
```BibTeX
@INPROCEEDINGS{10446420,
  author={Song, Tianyi and Cao, Jiuxin and Wang, Kun and Liu, Bo and Zhang, Xiaofeng},
  booktitle={ICASSP 2024 - 2024 IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP)}, 
  title={Causal-Story: Local Causal Attention Utilizing Parameter-Efficient Tuning for Visual Story Synthesis}, 
  year={2024},
  volume={},
  number={},
  pages={3350-3354},
  keywords={Training;Image quality;Visualization;Coherence;Signal processing;Acoustics;Speech processing;Training;Image synthesis;Diffusion model;Story visualization;Multi-modalities},
  doi={10.1109/ICASSP48485.2024.10446420}}

