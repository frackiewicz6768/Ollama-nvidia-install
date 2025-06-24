# Ollama-nvidia-install

Table of Contents

   1. Graphic card drivers installation
   3. Ollama installation
   4. Anythingllm installation
   5.  Additional Notes

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
```


