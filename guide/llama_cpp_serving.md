# LLAMA.CPP SERVING GUIDE
simple macOS guide for downloading GGUF models and serving them with llama.cpp

```sh
# llama.cpp command note
# llama-server is the server binary documented in the llama.cpp repo.
# llama serve is the newer wrapper command from the llama.app installer.
# both forms can serve models, but brew/source installs usually use llama-server.
```

```sh
# install on macOS with homebrew
brew install llama.cpp

# check the server binary
llama-server --help
```

```sh
# optional install from llama.app if you want the llama serve wrapper
curl -LsSf https://llama.app/install.sh | sh

# check the wrapper
llama --help
```

```sh
# make the model directory
mkdir -p /Users/nonresistant/Downloads/huggingface_models

# move into the model directory before downloading
cd /Users/nonresistant/Downloads/huggingface_models
```

```sh
# mac hardware suggestions
# 8 GB unified memory: use 1B to 4B Q4 models.
# 16 GB unified memory: use 7B to 8B Q4 models.
# 24 GB unified memory: use 14B Q4 models.
# 32 GB unified memory: use 14B comfortably, some 27B models with low context.
# 64 GB unified memory: use 32B Q4 models.
# 96 GB or more unified memory: use 70B Q4 models.
```

```sh
# model size notes
# Q4_K_M is a good first choice for local serving.
# 1B Q4 models are usually around 1 GB.
# 4B Q4 models are usually around 2.5 GB.
# 8B Q4 models are usually around 5 GB.
# 14B Q4 models are usually around 9 GB.
# 32B Q4 models are usually around 20 GB.
# leave extra memory for context, macOS, and other apps.
```

```sh
# download a small fast model, good for 8 GB Macs
wget -c -O gemma-3-1b-it-Q4_K_M.gguf \
  https://huggingface.co/ggml-org/gemma-3-1b-it-GGUF/resolve/main/gemma-3-1b-it-Q4_K_M.gguf

# download a balanced small model, good for 8 GB to 16 GB Macs
wget -c -O gemma-3-4b-it-Q4_K_M.gguf \
  https://huggingface.co/unsloth/gemma-3-4b-it-GGUF/resolve/main/gemma-3-4b-it-Q4_K_M.gguf

# download a strong general chat model, good for 16 GB Macs
wget -c -O Qwen3-8B-Q4_K_M.gguf \
  https://huggingface.co/unsloth/Qwen3-8B-GGUF/resolve/main/Qwen3-8B-Q4_K_M.gguf

# download a popular llama instruct model, good for 16 GB Macs
wget -c -O Meta-Llama-3.1-8B-Instruct-Q4_K_M.gguf \
  https://huggingface.co/bartowski/Meta-Llama-3.1-8B-Instruct-GGUF/resolve/main/Meta-Llama-3.1-8B-Instruct-Q4_K_M.gguf
```

```sh
# serve a downloaded model with the documented server binary
llama-server \
  -m /Users/nonresistant/Downloads/huggingface_models/Qwen3-8B-Q4_K_M.gguf \
  --host 127.0.0.1 \
  --port 8080 \
  -c 8192 \
  -ngl auto

# open the web ui
# http://127.0.0.1:8080

# openai-compatible base url
# http://127.0.0.1:8080/v1
```

```sh
# serve the same model with the llama.app wrapper command
llama serve \
  -m /Users/nonresistant/Downloads/huggingface_models/Qwen3-8B-Q4_K_M.gguf \
  --host 127.0.0.1 \
  --port 8080 \
  -c 8192 \
  -ngl auto
```

```sh
# serve directly from Hugging Face with llama-server
llama-server \
  -hf unsloth/Qwen3-8B-GGUF:Q4_K_M \
  --host 127.0.0.1 \
  --port 8080 \
  -c 8192

# serve directly from Hugging Face with the wrapper
llama serve \
  -hf unsloth/Qwen3-8B-GGUF:Q4_K_M \
  --host 127.0.0.1 \
  --port 8080 \
  -c 8192
```

```sh
# test the chat endpoint
curl http://127.0.0.1:8080/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "local-model",
    "messages": [
      {
        "role": "user",
        "content": "write a short haiku about local ai"
      }
    ],
    "temperature": 0.7
  }'
```

```sh
# use from coding tools
# llama.cpp server is OpenAI API compatible.
# set base url to http://127.0.0.1:8080/v1
# set api key to any placeholder value if the tool requires one.
# use model name local-model unless your tool asks for a specific display name.
# this works in tools that support custom OpenAI-compatible providers.
```

```sh
# common tuning notes
# lower -c to 4096 if memory is tight.
# use -ngl auto on Apple silicon to let llama.cpp choose Metal offload.
# use --host 0.0.0.0 only if other devices on your network need access.
# some Meta Llama downloads may require accepting the model license on Hugging Face.
```





==================
<br/>
copyright 2026 by sleet.near
