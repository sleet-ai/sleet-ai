# LLAMA.CPP SERVING GUIDE
simple commands to install llama.cpp, download GGUF models, and serve them locally

```sh
# make the model directory
mkdir -p /Users/nonresistant/Downloads/huggingface_models

# move into the model directory before downloading
cd /Users/nonresistant/Downloads/huggingface_models
```

```sh
# install llama.cpp on macOS or Linux
curl -LsSf https://llama.app/install.sh | sh

# check the commands are installed
llama --help
llama-server --help
```

```sh
# download a small fast model, good for quick testing
wget -c -O gemma-3-1b-it-Q4_K_M.gguf \
  https://huggingface.co/ggml-org/gemma-3-1b-it-GGUF/resolve/main/gemma-3-1b-it-Q4_K_M.gguf

# download a balanced small model
wget -c -O gemma-3-4b-it-Q4_K_M.gguf \
  https://huggingface.co/unsloth/gemma-3-4b-it-GGUF/resolve/main/gemma-3-4b-it-Q4_K_M.gguf

# download a strong general chat model
wget -c -O Qwen3-8B-Q4_K_M.gguf \
  https://huggingface.co/unsloth/Qwen3-8B-GGUF/resolve/main/Qwen3-8B-Q4_K_M.gguf

# download a popular llama instruct model
wget -c -O Meta-Llama-3.1-8B-Instruct-Q4_K_M.gguf \
  https://huggingface.co/bartowski/Meta-Llama-3.1-8B-Instruct-GGUF/resolve/main/Meta-Llama-3.1-8B-Instruct-Q4_K_M.gguf
```

```sh
# serve a downloaded model on localhost:8080
llama-server \
  -m /Users/nonresistant/Downloads/huggingface_models/Qwen3-8B-Q4_K_M.gguf \
  --host 127.0.0.1 \
  --port 8080 \
  -c 8192 \
  -ngl 99

# use -ngl 0 for CPU only
# use lower -c values if memory is tight
```

```sh
# test the local OpenAI-compatible chat endpoint
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
# serve directly from Hugging Face without manually downloading first
llama-server -hf ggml-org/gemma-3-1b-it-GGUF:Q4_K_M

# serve qwen3 directly from Hugging Face
llama-server -hf unsloth/Qwen3-8B-GGUF:Q4_K_M
```

```sh
# run a one-off terminal chat with a downloaded model
llama-cli \
  -m /Users/nonresistant/Downloads/huggingface_models/gemma-3-4b-it-Q4_K_M.gguf \
  -p "explain gguf in one paragraph"
```

```sh
# notes
# Q4_K_M is a good first quantization choice for size and quality.
# Q5_K_M usually gives better quality and uses more disk and memory.
# Some Meta Llama downloads may require accepting the model license on Hugging Face first.
```





==================
<br/>
copyright 2026 by sleet.near
