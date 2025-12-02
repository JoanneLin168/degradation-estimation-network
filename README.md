# Towards a General-Purpose Zero-Shot Synthetic Low-Light Image and Video Pipeline [McGE'25 Workshop]

**Authors**: _Joanne Lin, Crispian Morris, Ruirui Lin, Fan Zhang, David Bull, Nantheera Anantrasirichai_

**Institution**: Visual Information Laboratory, University of Bristol, United Kingdom

[[`Project Page`]([https://joannelin168.github.io/low-light/ELVIS/](https://joannelin168.github.io/low-light/DEN/))][[`Paper`](https://dl.acm.org/doi/10.1145/3746278.3759376)][[`arXiv`](https://arxiv.org/abs/2504.12169)]

## Setup
### Dependencies
Create and run conda environment:
```
conda env create -f environment.yml
conda activate DEN
```

### Dataset
Please download YouTube-VOS dataset [here](https://youtube-vos.org/dataset/vos/).

> [!WARNING]
> Please ensure you store YouTube-VOS in a different folder and create soft link with training set in `data/` as `valid_all_frames/` will be overwritten when running `tools/create_valid_set.py`

Then run the following scripts to generate synthetic noisy data for evaluation:
```
cd tools
python create_random_noises.py
python create_valid_set.py -i <path-to-val-data> -o ./data/val_all_frames
ln -s <path-to-train-data> ./data/train_all_frames
```

Your directory tree should look something like this:
```
degradation-estimation-network/
├── data/
│ ├── train_all_frames/
│ | └── JPEGImages/
│ | | ├── ...
│ └── valid_all_frames/
│ | └── JPEGImages/
│ | | ├── ...
├── dataset/
│ ├── ...
├── models/
│ ├── ...
├── src/
│ ├── ...
├── tools/
│ ├── ...
├── environment.yml
├── LICENSE
├── README.md
└── main.py
```

## Train
Run the following command to train our model:
```
python train.py
```

## Inference
Currently not implemented yet. Feel free to use our released [weights](https://github.com/JoanneLin168/degradation-estimation-network/releases/download/v1.0/best.pt).

## Known bugs
If you see a warning message like this:
```
[W C:\cb\pytorch_1000000000000\work\torch\csrc\CudaIPCTypes.cpp:15] Producer process has been terminated before all shared CUDA tensors released. See Note [Sharing CUDA tensors]
```
add the flag `--workers 0` to the command to fix this.

## Citation
If you use our work in your research, please cite using the following BibTeX entry:
```
@inproceedings{lin2025den,
  author = {Lin, Joanne and Morris, Crispian and Lin, Ruirui and Zhang, Fan and Bull, David and Anantrasirichai, Nantheera},
  title = {Towards a General-Purpose Zero-Shot Synthetic Low-Light Image and Video Pipeline},
  year = {2025},
  isbn = {9798400720604},
  publisher = {Association for Computing Machinery},
  address = {New York, NY, USA},
  url = {https://doi.org/10.1145/3746278.3759376},
  doi = {10.1145/3746278.3759376},
  booktitle = {Proceedings of the 3rd International Workshop on Multimedia Content Generation and Evaluation: New Methods and Practice},
  pages = {3–11},
  numpages = {9},
  keywords = {synthetic data, low-light, degradations, general-purpose, zero-shot, self-supervised},
  location = {Ireland},
  series = {McGE '25}
}
```
