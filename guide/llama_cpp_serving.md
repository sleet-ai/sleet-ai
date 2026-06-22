# LLAMA.CPP SERVING GUIDE
simple macOS guide for serving GGUF models directly from Hugging Face with llama.cpp

```sh
# command note
# this guide uses the llama.app wrapper command:
# llama serve -hf repo/name:quant --host 127.0.0.1 --port 8080 -c context
# the -hf flag downloads and caches the selected GGUF automatically.
```

```sh
# install the wrapper on macOS
curl -LsSf https://llama.app/install.sh | sh
llama --help
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
# model notes
# Q4_K_M is a good first choice for local serving.
# file sizes below are for the Q4_K_M GGUF file.
# context is the GGUF metadata context length, not the chosen -c value.
# larger -c values use more memory because the KV cache grows with context.
```

```sh
# gemma 3 1b it
# repo: ggml-org/gemma-3-1b-it-GGUF
# file: gemma-3-1b-it-Q4_K_M.gguf
# size: 806,058,240 bytes, about 0.81 GB.
# context: 32,768 tokens.
# best fit: very small and fast; good first pick for 8 GB Macs.
llama serve -hf ggml-org/gemma-3-1b-it-GGUF:Q4_K_M --host 127.0.0.1 --port 8080 -c 8192
```

```sh
# gemma 3 4b it
# repo: unsloth/gemma-3-4b-it-GGUF
# file: gemma-3-4b-it-Q4_K_M.gguf
# size: 2,489,894,016 bytes, about 2.49 GB.
# context: 131,072 tokens.
# best fit: stronger small model; good for 8 GB to 16 GB Macs.
llama serve -hf unsloth/gemma-3-4b-it-GGUF:Q4_K_M --host 127.0.0.1 --port 8080 -c 8192
```

```sh
# qwen3 8b
# repo: unsloth/Qwen3-8B-GGUF
# file: Qwen3-8B-Q4_K_M.gguf
# size: 5,027,784,512 bytes, about 5.03 GB.
# context: 40,960 tokens.
# best fit: strong general chat and reasoning model; good for 16 GB Macs.
llama serve -hf unsloth/Qwen3-8B-GGUF:Q4_K_M --host 127.0.0.1 --port 8080 -c 8192
```

```sh
# meta llama 3.1 8b instruct
# repo: bartowski/Meta-Llama-3.1-8B-Instruct-GGUF
# file: Meta-Llama-3.1-8B-Instruct-Q4_K_M.gguf
# size: 4,920,739,232 bytes, about 4.92 GB.
# context: 131,072 tokens.
# best fit: popular instruct model; good for 16 GB Macs.
llama serve -hf bartowski/Meta-Llama-3.1-8B-Instruct-GGUF:Q4_K_M --host 127.0.0.1 --port 8080 -c 8192
```

```sh
# web ui: http://127.0.0.1:8080
# openai-compatible base url: http://127.0.0.1:8080/v1
# lower -c to 4096 if memory is tight.
# raise -c only when you need longer prompts and have memory available.
# use --host 0.0.0.0 only if other devices on your network need access.
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
```

==================
<br/>
copyright 2026 by sleet.near
