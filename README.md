# vllm
https://docs.vllm.ai/en/latest/
```
#modelscope download --model Qwen/Qwen3.5-9B --local_dir ./models/Qwen3.5-9B

docker run --rm -it --name qwen35 \
        --gpus all --ipc=host --shm-size=16g -p 8000:8000 \
        -v $PWD/models:/models:ro \
        -e NCCL_P2P_DISABLE=0 -e NCCL_IB_DISABLE=1 \
        -e VLLM_API_LOG=1 -e VLLM_LOGGING_LEVEL=INFO \
        vllm/vllm-openai \
        --model /models/Qwen3.5-9B \
        --enable-auto-tool-choice \
        --tool-call-parser qwen3_coder \
        --reasoning-parser qwen3 \
        --served-model-name Qwen3.5-9B \
        --tensor-parallel-size 1 --max-model-len 32768 --kv-cache-dtype fp8
        --gpu-memory-utilization 0.85 --max-num-seqs 4 --max-num-batched-tokens 8192 \
        --language-model-only --enable-prefix-caching \
        --default-chat-template-kwargs '{"enable_thinking": true}' \
        --host 0.0.0.0 --port 8000


curl -X POST "http://127.0.0.1:8000/v1/chat/completions"  \
       -H "Content-Type: application/json"  \
       --data '{
                "model": "Qwen3.5-9B",
                "messages": [{
                                "role": "user",
                                "content": "日本是美国的吗"
                            }]
              }'
```
## opencode
```
    "vllm": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "vllm (ROG)",
      "options": {
        "baseURL": "http://192.168.0.111:8000/v1",
      },
      "models": {
        "Qwen3.5-9B": {
          "name": "Qwen3.5 9B",
          "modalities": {
            "input": ["text", "image"],
            "output": ["text"]
          },
          "limit": {
            "context": 32768,
            "output": 4096
          }
        }
      }
    },
```

## Claude Code CLI
```
export ANTHROPIC_BASE_URL=https://api.deepseek.com/anthropic
export ANTHROPIC_AUTH_TOKEN=DEEPSEEK_API_KEY
export API_TIMEOUT_MS=600000
export ANTHROPIC_MODEL=deepseek-chat
export ANTHROPIC_SMALL_FAST_MODEL=deepseek-chat
export CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC=1
```
