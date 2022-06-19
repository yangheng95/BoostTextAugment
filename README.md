# Boosting Data Augmentation for Text Classification

## Notice

This tool depends on the [PyABSA](https://github.com/yangheng95/PyABSA),
and is integrated with the [ABSADatasets](https://github.com/yangheng95/ABSADatasets).

To augment your own dataset, you need to prepare your dataset according to **ABSADatasets**.
Refer to the [instruction to process](https://github.com/yangheng95/ABSADatasets)
or [annotate your dataset](https://github.com/yangheng95/ABSADatasets/tree/v1.2/DPT).

## Install BoostAug

### Install from pip

```bash
pip install BoostAug
```

### Install from source

```bash
git clone https://github.com/yangheng95/BoostingAugABSA
cd BoostingAugABSA
pip install .
```

## Quick Start

We made a package BoostAug which can helps while using our code, here are the examples for using BoostAug to improve
aspect-level polarity classification and sentence-level text classification

## Experiments

## MUST READ

- If the augmentation traning is terminated by accidently or you want to rerun augmentation, set `rewrite_cache=False`
  in augmentation.
- If you have many datasets, run augmentation for differnet datasets IN SEPARATE FOLDER, otherwise `IO OPERATION`
  may CORRUPT other datasets

The experimental results can be reproduced by running the `main_experiments_absc.py` or `main_experiments_tc.py`
in the [experiment_absc](experiment_absc) and [expeirment_tc](experiment_tc) folders.

If there is no enough resource to run augmentation, we have done some augmentation and
prepared some augmentation sets in the dataset folders, please set `rewrite_cache=False` to run training on these
augmentation sets.
e.g.,

### Import BoostAug

```python3
import shutil
import autocuda
import findfile
import random
import warnings

from boost_aug import BoostingAug, AugmentBackend

from pyabsa.functional import APCConfigManager
from pyabsa.functional import ABSADatasetList
from pyabsa.functional import APCModelList

warnings.filterwarnings('ignore')
```

### Create a BoostingAugmenter

```python3
aug_backend = AugmentBackend.EDA

# BoostingAugmenter = BoostingAug(AUGMENT_BACKEND=aug_backend, device='cuda')
BoostingAugmenter = BoostingAug(AUGMENT_BACKEND=aug_backend, device=autocuda.auto_cuda())
```

### Augmentation and Training

```python3
BoostingAugmenter.apc_boost_augment(config,  # BOOSTAUG
                                    dataset,
                                    train_after_aug=True,  # comment this line to perform augmentation without training
                                    rewrite_cache=False, # use pre-augmented datasets for training to evaluate performance
                                    )

```

# Notice

This is the draft code, so do not perform cross-boosting on different dataset in the same folder, which will raise some
Exception
