# [MDF-Polyp](https://github.com/fuyou-99/MDF_Polyp)

Official repository for MDF-Polyp: Multi-Domain Fusion Network for Enhanced Polyp Segmentation in Colonoscopy Images

## Installation 

Requirements: `Ubuntu 20.04`, `CUDA 12.1`

1. Create a virtual environment: `conda create -n MDF-Polyp python=3.10 -y` and `conda activate MDF-Polyp `
2. Install [Pytorch](https://pytorch.org/get-started/previous-versions/#linux-and-windows-4) 2.2.2: `pip install torch==2.2.2 torchvision==0.17.2 torchaudio==2.2.2 --index-url https://download.pytorch.org/whl/cu121`
3. Install [Mamba](https://github.com/state-spaces/mamba): `pip install causal-conv1d>=1.2.0` and `pip install mamba-ssm --no-cache-dir`
4. Download code: `git clone https://github.com/fuyou-99/MDF_Polyp`
5. `cd MDF-Polyp/MDF-Polyp` and run `pip install -e .`


sanity test: Enter python command-line interface and run

```bash
import torch
import mamba_ssm
```

![network](https://github.com/fuyou-99/MDF_Polyp/blob/main/assets/MDF-Polyp-network.png)


### Preprocessing

```bash
nnUNetv2_plan_and_preprocess -d DATASET_ID --verify_dataset_integrity
```

### Train models

```bash
nnUNetv2_train DATASET_ID 2d all -tr nnUNetTrainerMDF_Polyp
```


## Inference

- Predict testing cases with `nnUNetTrainerMDF_Polyp` model

```bash
nnUNetv2_predict -i INPUT_FOLDER -o OUTPUT_FOLDER -d DATASET_ID -c CONFIGURATION -f all -tr nnUNetTrainerMDF_Polyp --disable_tta
```


## Remarks

```python
# An example to set other data path,
base = '/home/user_name/Documents/MDF_Polyp/data'
nnUNet_raw = join(base, 'nnUNet_raw') # or change to os.environ.get('nnUNet_raw')
nnUNet_preprocessed = join(base, 'nnUNet_preprocessed') # or change to os.environ.get('nnUNet_preprocessed')
nnUNet_results = join(base, 'nnUNet_results') # or change to os.environ.get('nnUNet_results')
```


## Acknowledgements

We acknowledge all the authors of the employed public datasets, allowing the community to use these valuable resources for research purposes. We also thank the authors of [nnU-Net](https://github.com/MIC-DKFZ/nnUNet) and [Mamba](https://github.com/state-spaces/mamba) for making their valuable code publicly available.

