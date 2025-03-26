# Claude Code with Deepseek Models 🧙‍♂️🤖

A proxy server that lets you use Claude Code with Deepseek models like deepseek-chat and deepseek-coder. Save on API costs while maintaining excellent code assistant capabilities.

## Quick Start ⚡

### Prerequisites

- Deepseek API key 🔑

### Setup 🛠️

1. **Clone this repository**:
   ```bash
   git clone https://github.com/kevinnbass/claude-code-deepseek.git
   cd claude-code-deepseek
   ```

2. **Install UV**:
   ```bash
    curl -LsSf https://astral.sh/uv/install.sh | sh
   ```

3. **Configure your API keys**:
   Create a `.env` file with:
   ```
   DEEPSEEK_API_KEY=your-deepseek-key
   # Optional: customize which models are used
   # BIG_MODEL=deepseek-chat
   # SMALL_MODEL=deepseek-chat
   ```

4. **Start the proxy server**:
   ```bash
   uv run uvicorn server:app --host 0.0.0.0 --port 8082
   ```

### Using with Claude Code 🎮

1. **Install Claude Code** (if you haven't already):
   ```bash
   npm install -g @anthropic-ai/claude-code
   ```

2. **Connect to your proxy**:
   ```bash
   ANTHROPIC_BASE_URL=http://127.0.0.1:8082 claude
   ```
   
   Note: Using the IP address directly (127.0.0.1) instead of localhost can resolve connection issues.

3. **That's it!** Your Claude Code client will now use Deepseek models through the proxy. 🎯

## Model Mapping 🗺️

The proxy automatically maps Claude models to Deepseek models:

| Claude Model | Deepseek Model |
|--------------|----------------|
| haiku | deepseek-chat (default) |
| sonnet | deepseek-chat (default) |

### Customizing Model Mapping

You can customize which Deepseek models are used via environment variables:

- `BIG_MODEL`: The Deepseek model to use for Claude Sonnet models (default: "deepseek-chat")
- `SMALL_MODEL`: The Deepseek model to use for Claude Haiku models (default: "deepseek-chat")

Add these to your `.env` file to customize:
```
DEEPSEEK_API_KEY=your-deepseek-key
BIG_MODEL=deepseek-chat
SMALL_MODEL=deepseek-coder
```

Or set them directly when running the server:
```bash
BIG_MODEL=deepseek-chat SMALL_MODEL=deepseek-coder uv run uvicorn server:app --host 0.0.0.0 --port 8082
```

## How It Works 🧩

This proxy works by:

1. **Receiving requests** in Anthropic's API format 📥
2. **Translating** the requests to Deepseek format via LiteLLM 🔄
3. **Sending** the translated request to Deepseek 📤
4. **Converting** the response back to Anthropic format 🔄
5. **Returning** the formatted response to the client ✅

The proxy handles both streaming and non-streaming responses, maintaining compatibility with all Claude clients. 🌊

## Token Limit ⚠️

Deepseek models have a maximum token limit of 8192, which is automatically enforced by the proxy.

## Performance Comparison

Based on testing, Deepseek models have comparable capabilities to Claude models but with different response times:

| Feature | Response Time Comparison |
|---------|--------------------------|
| Simple text generation | Deepseek ~5-7s vs Claude ~1-2s |
| Complex reasoning | Deepseek ~12-15s vs Claude ~2-3s |
| Code generation | Deepseek ~15-18s vs Claude ~3-4s |
| Tool usage | Deepseek ~5-6s vs Claude ~1-2s |

The proxy includes Chain-of-Thought prompting for improved reasoning capabilities with Deepseek models.

## Detailed Capabilities

For a comprehensive comparison between Claude and Deepseek model capabilities, please see the [CAPABILITIES.md](CAPABILITIES.md) file in this repository.

## Contributing 🤝

Contributions are welcome! Please feel free to submit a Pull Request. 🎁
