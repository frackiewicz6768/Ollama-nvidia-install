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
```
curl -fsSL https://ollama.com/install.sh | sh
ollama --version
ollama version is 0.9.2
```
### Ollama service
```
sudo nano /etc/systemd/system/ollama.service

[Unit]
Description=Ollama Service
After=network-online.target

[Service]
ExecStart=/usr/bin/ollama serve
User=ollama
Group=ollama
Restart=always
RestartSec=3

[Install]
WantedBy=default.target

sudo systemctl daemon-reexec     
sudo systemctl daemon-reload  
sudo systemctl enable ollama 
sudo systemctl start ollama 


```
## Anythingllm installation

Prepare docker-compose.yaml
```
services:
  anythingllm:
    image: mintplexlabs/anythingllm:latest
    container_name: anythingllm
    ports:
      - "3001:3001"
    volumes:
      - ./storage:/app/server/storage
    cap_add:
      - SYS_ADMIN
    environment:
      - STORAGE_DIR=/app/server/storage
    user: "1005:1005" # custom user
    networks:
      anything-llm:
    restart: unless-stopped

networks:
  anything-llm:
    driver: bridge
```
Next start anythinll by using a command:
```
docker compose up -d
docker ps
```
After confirmation that everytning works fine download desired models:

```
ollama help
Large language model runner

Usage:
  ollama [flags]
  ollama [command]

Available Commands:
  serve       Start ollama
  create      Create a model from a Modelfile
  show        Show information for a model
  run         Run a model
  stop        Stop a running model
  pull        Pull a model from a registry
  push        Push a model to a registry
  list        List models
  ps          List running models
  cp          Copy a model
  rm          Remove a model
  help        Help about any command

Flags:
  -h, --help      help for ollama
  -v, --version   Show version information
```
You can use sucha script to download models:
```
#!/usr/bin/env bash
set -e

MODELS=(
  phi3 qwen2 mxbai-embed-large olmo2 deepseek-v3 qwq bge-m3 llama2-uncensored
  llava-llama3 mixtral mistral-small smollm2 starcoder2 deepseek-coder-v2
  deepseek-coder snowflake-arctic-embed codegemma all-minilm phi
  dolphin-mixtral openthinker orca-mini wizardlm2 dolphin-mistral
  dolphin-llama3 codestral smollm command-r hermes3 phi3.5 yi zephyr
  granite-code moondream wizard-vicuna-uncensored phi4-mini starcoder
  vicuna mistral-openorca openchat codegeex4 deepseek-v2
)

TAG="latest"

echo "Downloading models from Ollama Library..."

for MODEL in "${MODELS[@]}"; do
  echo -e "\n🔁 Pobieram: $MODEL:$TAG"
  ollama pull "$MODEL:$TAG" || echo "Not possible: $MODEL"
done

echo -e "\n✅ Ready!"
```

## Additional Notes
