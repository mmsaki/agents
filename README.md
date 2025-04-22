# Minimal Local Agent

My setup:

- 2017 MacBook Pro 2.9 GHz Quad-Core Intel Core i7
- 16 GB Ram
- 512 GB Storage

## Setup

> [!NOTE]
> Download [ollama.com/download](https://ollama.com/download)

Download a model from [ollama.com/search](https://ollama.com/search)

```sh
ollama pull qwen2:7b
```

Start ollama

```sh
ollama serve
```

## Environment

> [!NOTE]
> Install uv python package manager [astral.sh](https://docs.astral.sh/uv/getting-started/installation/)

Setup virtual environment

```sh
# clone this repo
git clone https://github.com/mmsaki/agents.git

# enter project directory
cd agents

# setup local environment
uv venv

# activate local environment
source .venv/bin/activate
```

## Initialize model

Initialize model with `LiteLLM` in [./src/agents/\_\_init\_\_.py](./src/agents/__init__.py)

```py
from smolagents import LiteLLMModel

model = LiteLLMModel(
    model_id="ollama_chat/qwen2:7b",  # Or try other Ollama-supported models
    api_base="http://127.0.0.1:11434",  # Default Ollama local server
    num_ctx=8192,
)

```

## Start agent

Calling agent in python

```py
messages = [
    {"role": "user", "content": [{"type": "text", "text": "Hello, how are you?"}]}
]
model(messages)
```

Run

```sh
uv run agents
```

Output

```sh
(agents) 🐇 uv run agents
ChatMessage(role=<MessageRole.ASSISTANT: 'assistant'>, content="As an AI language model, I don't have feelings like humans do, but I'm func
tioning properly and ready to assist you with any questions or tasks you might have! How can I help you today?", tool_calls=None, raw=Model
Response(id='chatcmpl-c29f12fa-b516-4548-8ef7-96f2cf2e70e9', created=1745245459, model='ollama_chat/qwen2:7b', object='chat.completion', sy
stem_fingerprint=None, choices=[Choices(finish_reason='stop', index=0, message=Message(content="As an AI language model, I don't have feeli
ngs like humans do, but I'm functioning properly and ready to assist you with any questions or tasks you might have! How can I help you tod
ay?", role='assistant', tool_calls=None, function_call=None, provider_specific_fields=None))], usage=Usage(completion_tokens=42, prompt_tok
ens=25, total_tokens=67, completion_tokens_details=None, prompt_tokens_details=None)))
(agents) 🐇 
```
