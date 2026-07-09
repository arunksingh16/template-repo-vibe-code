# Github copilot Specifics


BYOM - https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/use-byok-models

### How to use it with vLLM endpoint 
```
export COPILOT_OFFLINE=true
export COPILOT_PROVIDER_BASE_URL=https://<vllm-endpoint>/v1
export COPILOT_PROVIDER_API_KEY=YOUR-OPENAI-API-KEY
export COPILOT_MODEL=YOUR-MODEL-NAME
```
