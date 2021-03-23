# LaneAF: Robust Multi-Lane Detection with Affinity Fields

This repository contains Pytorch code for training and testing LaneAF lane detection models introduced in [this paper](http://cvrr.ucsd.edu/publications/2021/LaneAF.pdf).

## Installation
1) Clone this repository
2) Install Anaconda
3) Create a virtual environment and install all dependencies:
```shell
conda create -n laneaf pip python=3.6
source activate laneaf
pip install numpy scipy matplotlib pillow tqdm kmeans-pytorch scikit-learn
conda install -c menpo opencv
pip install https://download.pytorch.org/whl/cu101/torch-1.7.0%2Bcu101-cp36-cp36m-linux_x86_64.whl
pip install https://download.pytorch.org/whl/cu101/torchvision-0.8.1%2Bcu101-cp36-cp36m-linux_x86_64.whl
source deactivate
```
You can alternately find your desired torch/torchvision wheel from [here](https://download.pytorch.org/whl/torch_stable.html).

4) Clone and make DCNv2:
```shell
cd models/dla
git clone https://github.com/lbin/DCNv2.git
cd DCNv2
./make.sh
```

## TuSimple
The entire [TuSimple dataset](https://github.com/TuSimple/tusimple-benchmark/issues/3) should be downloaded and organized as follows:
```plain
└── TuSimple
    ├── clips
    |   └── .
    |   └── .
    ├── label_data_0313.json
    ├── label_data_0531.json
    ├── label_data_0601.json
    ├── test_tasks_0627.json
    ├── test_baseline.json
    └── test_label.json
```
<!---
The model requires ground truth affinity fields during training. You can generate these for the entire dataset as follows:
```shell
source activate laneaf # activate virtual environment
python datasets/tusimple.py --dataset-dir=/path/to/TuSimple/
source deactivate # exit virtual environment
```
-->

### Training
LaneAF models can be trained on the TuSimple as follows:
```shell
source activate laneaf # activate virtual environment
python train_tusimple.py --dataset-dir=/path/to/TuSimple/ --random-transforms
source deactivate # exit virtual environment
```
Config files, logs, results and snapshots from running the above scripts will be stored in the `LaneAF/experiments/tusimple` folder by default.

### Inference
Trained LaneAF models can be run on the TuSimple test set as follows:
```shell
source activate laneaf # activate virtual environment
python infer_tusimple.py --dataset-dir=/path/to/TuSimple/ --snapshot=/path/to/trained/model/snapshot --save-viz
source deactivate # exit virtual environment
```
This will generate outputs in the TuSimple format and also produce benchmark metrics using their [official implementation](https://github.com/TuSimple/tusimple-benchmark/tree/master/doc/lane_detection).

## CULane
The entire [CULane dataset](https://xingangpan.github.io/projects/CULane.html) should be downloaded and organized as follows:
```plain
└── CULane
    ├── driver_*_*frame/
    ├── laneseg_label_w16/
    ├── laneseg_label_w16_test/
    └── list/
```
<!---
The model requires ground truth affinity fields during training. You can generate these for the entire dataset as follows:
```shell
source activate laneaf # activate virtual environment
python datasets/culane.py --dataset-dir=/path/to/CULane/
source deactivate # exit virtual environment
```
-->

### Training
LaneAF models can be trained on the CULane as follows:
```shell
source activate laneaf # activate virtual environment
python train_culane.py --dataset-dir=/path/to/CULane/ --random-transforms
source deactivate # exit virtual environment
```
Config files, logs, results and snapshots from running the above scripts will be stored in the `LaneAF/experiments/culane` folder by default.

### Inference
Trained LaneAF models can be run on the CULane test set as follows:
```shell
source activate laneaf # activate virtual environment
python infer_culane.py --dataset-dir=/path/to/CULane/ --snapshot=/path/to/trained/model/snapshot --save-viz
source deactivate # exit virtual environment
```
This will generate outputs in the CULane format. You can then use their [official code](https://github.com/XingangPan/SCNN) to evaluate the model on the CULane benchmark.

## Pre-trained Weights
You can download our pre-trained model weights using [this link](https://drive.google.com/file/d/1GJoVQfDyxhUT8Y5EqTRV9PX3WWckfxWG/view?usp=sharing).

<!---
## Citation
If you find our code and/or models useful in your research, please consider citing the following papers:

    @article{abualsaudlaneaf,
        title={LaneAF: Robust Multi-Lane Detection with Affinity Fields},
        author={Abualsaud, Hala and Liu, Sean and Lu, David and Situ, Kenny and Rangesh, Akshay and Trivedi, Mohan M}
    }
-->
