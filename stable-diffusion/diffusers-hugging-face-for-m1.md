## Install & Use 

https://wandb.ai/morgan/stable-diffusion/reports/Running-Stable-Diffusion-on-an-Apple-M1-Mac-with-Hugging-Face-Diffusers

## Sequence 
- conda env 만들 

```python
$ conda create -n SD-diffusers python=3.8.8
```

- 토치 설치 

```python
$ conda install pytorch torchvision torchaudio -c pytorch-nightly
```

- 프랜스포머 설치 
```python
$ conda install transformers
```

- diffusers 설치 
```python
$ conda install -c conda-forge diffusers
```

- fastcore 설치 
```python
$ conda install fastcore
```

- 허깅 페이스 로그인 
```python
$ huggingface-cli login
```

### 기타 
나머지는 위에 링크한 페이지를 참고하면 된다. 

