# PAFDLA models for Lane Detection

This repository contains the Pytorch code for training and testing all PAFDLA lane detection models.

## Installation
1) Clone this repository
2) Install Anaconda
3) Create a virtual environment and install all dependencies:
```shell
conda create -n PAFDLA pip python=3.6
source activate PAFDLA
pip install numpy scipy matplotlib pillow tqdm kmeans-pytorch scikit-learn
conda install -c menpo opencv
pip install https://download.pytorch.org/whl/cu100/torch-1.2.0-cp36-cp36m-manylinux1_x86_64.whl
pip install https://download.pytorch.org/whl/cu100/torchvision-0.3.0-cp36-cp36m-linux_x86_64.whl
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
The model requires ground truth affinity fields during training. You can generate these for the entire dataset as follows:
```shell
source activate PAFDLA # activate virtual environment
python datasets/tusimple.py --dataset-dir=/path/to/TuSimple/
source deactivate # exit virtual environment
```

### Training
PAFDLA models can be trained on the TuSimple as follows:
```shell
source activate PAFDLA # activate virtual environment
python train_tusimple.py --dataset-dir=/path/to/TuSimple/
source deactivate # exit virtual environment
```
Config files, logs, results and snapshots from running the above scripts will be stored in the `PAFDLA/experiments` folder by default.

### Inference
Trained PAFDLA models can be run on the TuSimple test set as follows:
```shell
source activate PAFDLA # activate virtual environment
python infer_tusimple.py --dataset-dir=/path/to/TuSimple/ --snapshot=/path/to/trained/model/snapshot
source deactivate # exit virtual environment
```

## CULane
The entire [CULane dataset](https://xingangpan.github.io/projects/CULane.html) should be downloaded and organized as follows:
```plain
└── CULane
    ├── driver_*_*frame/
    ├── laneseg_label_w16/
    ├── laneseg_label_w16_test/
    └── list/
```
The model requires ground truth affinity fields during training. You can generate these for the entire dataset as follows:
```shell
source activate PAFDLA # activate virtual environment
python datasets/culane.py --dataset-dir=/path/to/CULane/
source deactivate # exit virtual environment
```

### Training
PAFDLA models can be trained on the CULane as follows:
```shell
source activate PAFDLA # activate virtual environment
python train_culane.py --dataset-dir=/path/to/CULane/
source deactivate # exit virtual environment
```
Config files, logs, results and snapshots from running the above scripts will be stored in the `PAFDLA/experiments` folder by default.

### Inference
Trained PAFDLA models can be run on the CULane test set as follows:
```shell
source activate PAFDLA # activate virtual environment
python infer_culane.py --dataset-dir=/path/to/CULane/ --snapshot=/path/to/trained/model/snapshot
source deactivate # exit virtual environment
```
