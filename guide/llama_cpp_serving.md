# LLAMA.CPP SERVING GUIDE
simple macOS guide for downloading GGUF models and serving them with llama.cpp

```sh
# command note
# llama-server is the server binary documented in the llama.cpp repo.
# llama serve is the wrapper command shown by the llama.app installer.
# use llama-server for homebrew/source installs, or llama serve if you installed llama.app.
```

```sh
# install on macOS with homebrew
brew install llama.cpp wget

# check the documented server binary
llama-server --help

# optional wrapper install if you want llama serve
curl -LsSf https://llama.app/install.sh | sh
llama --help
```

```sh
# make and enter the model directory
mkdir -p /Users/nonresistant/Downloads/huggingface_models
cd /Users/nonresistant/Downloads/huggingface_models
```

```sh
# mac hardware suggestions
# 8 GB unified memory: 1B to 4B Q4 models.
# 16 GB unified memory: 7B to 8B Q4 models.
# 24 GB unified memory: 14B Q4 models.
# 32 GB unified memory: 14B comfortably, some 27B with low context.
# 64 GB unified memory: 32B Q4 models.
# 96 GB or more unified memory: 70B Q4 models.
```

```sh
# model size notes
# Q4_K_M is a good first choice for local serving.
# 1B Q4 is around 1 GB, 4B Q4 is around 2.5 GB, 8B Q4 is around 5 GB.
# 14B Q4 is around 9 GB, 32B Q4 is around 20 GB.
# leave extra memory for context, macOS, and other apps.
```

```sh
# small fast model, good for 8 GB Macs
wget -c -O gemma-3-1b-it-Q4_K_M.gguf \
  https://huggingface.co/ggml-org/gemma-3-1b-it-GGUF/resolve/main/gemma-3-1b-it-Q4_K_M.gguf

# balanced small model, good for 8 GB to 16 GB Macs
wget -c -O gemma-3-4b-it-Q4_K_M.gguf \
  https://huggingface.co/unsloth/gemma-3-4b-it-GGUF/resolve/main/gemma-3-4b-it-Q4_K_M.gguf

# strong general chat model, good for 16 GB Macs
wget -c -O Qwen3-8B-Q4_K_M.gguf \
  https://huggingface.co/unsloth/Qwen3-8B-GGUF/resolve/main/Qwen3-8B-Q4_K_M.gguf

# popular llama instruct model, good for 16 GB Macs
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

# web ui: http://127.0.0.1:8080
# openai-compatible base url: http://127.0.0.1:8080/v1
```

```sh
# same server with the llama.app wrapper command
llama serve \
  -m /Users/nonresistant/Downloads/huggingface_models/Qwen3-8B-Q4_K_M.gguf \
  --host 127.0.0.1 \
  --port 8080 \
  -c 8192 \
  -ngl auto
```

```sh
# serve directly from Hugging Face without manual wget
llama-server -hf unsloth/Qwen3-8B-GGUF:Q4_K_M --host 127.0.0.1 --port 8080 -c 8192

# wrapper version
llama serve -hf unsloth/Qwen3-8B-GGUF:Q4_K_M --host 127.0.0.1 --port 8080 -c 8192
```

```sh
# test the OpenAI-compatible chat endpoint
curl http://127.0.0.1:8080/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{"model":"local-model","messages":[{"role":"user","content":"write a short haiku about local ai"}]}'
```

```sh
# use from coding tools
# set openai-compatible base url to http://127.0.0.1:8080/v1
# set api key to any placeholder value if the tool requires one.
# use model name local-model unless your tool asks for a specific name.
# lower -c to 4096 if memory is tight.
# use --host 0.0.0.0 only if other devices on your network need access.
```

==================
<br/>
copyright 2026 by sleet.near
