# What 
- m1에서 pytorch 인스톨 

# Where 
[Weights & Biases (wandb.ai)](https://wandb.ai/capecape/pytorch-M1Pro/reports/PyTorch-Runs-On-the-GPU-of-Apple-M1-Macs-Now---VmlldzoyMDMyNzMz)
[apple_m1_pro_python/pytorch at main · tcapelle/apple_m1_pro_python (github.com)](https://github.com/tcapelle/apple_m1_pro_python/tree/main/pytorch)

# How 
## Prerequisites 
- conda & mamba are properly installed 
- setup env for pytorch based on python 10 
- activate env 

## Install

```bash
? pip install --pre torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/nightly/cpu
? pip install wandb tqdm
```

## Check 

```bash
import torch

torch.__version__
>>> '1.12.0.dev20220518'

torch.tensor([1,2,3], device="mps")
```

## Implement 
- change your direc to `pytorch`
```bash
? python train_pets.py --device="mps"
```

# Misc 

## GPU 활성 상태 체크 
- 찾기 "활성 상태 보기"
- 메뉴 -> 윈도우 -> GPU 기록 

