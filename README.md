# vllm
https://docs.vllm.ai/en/latest/

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
