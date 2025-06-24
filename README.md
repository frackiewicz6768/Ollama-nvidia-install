# Ollama-nvidia-install

Table of Contents

1. [Graphic card drivers installation](#graphic-card-drivers-installation)  
2. [Ollama installation](#ollama-installation)  
3. [Anythingllm installation](#anythingllm-installation)  
4. [Additional Notes](#additional-notes)


## Graphic card drivers installation

###  Graphic card detection

```
lspci | grep -i vga
65:00.0 VGA compatible controller: NVIDIA Corporation GA102GL [A6000] (rev a1)
```
For NVIDIA RTX A6000 on ubuntu best drivers are from 525 series or newer. We try to install 535 stable.

```
sudo ubuntu-drivers install nvidia:535
reboot
nvidia-smi
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 550.54.14    Driver Version: 550.54.14    CUDA Version: 12.4     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  RTX A6000           Off  | 00000000:65:00.0 Off |                  Off |
| 30%   40C    P8    35W / 300W |     300MiB / 49152MiB |     5%      Default  |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A      1234      C   python3                            300MiB |
+-----------------------------------------------------------------------------+

```
## Ollama installation

## Anythingllm installation

## Additional Notes
