# StemSplit

**AI-powered audio stem separation and noise removal — as an API, CLI, and integrations.**

[stemsplit.io](https://stemsplit.io) &nbsp;·&nbsp; [API docs](https://stemsplit.io/docs/api) &nbsp;·&nbsp; [Pricing](https://stemsplit.io/pricing)

---

Separate any song into vocals, drums, bass, piano, guitar, and other stems — or remove background noise from voice recordings — without managing your own ML infrastructure. Powered by [HTDemucs](https://github.com/adefossez/demucs) and [DeepFilterNet](https://github.com/Rikorose/DeepFilterNet) on GPU.

## Open-source packages

| Package | Install | What it does | Docs |
|---------|---------|--------------|------|
| [stemsplit-mcp](https://github.com/StemSplit/stemsplit-mcp) | `npx -y stemsplit-mcp` | MCP server — stem separation and voice cleaning inside Claude Desktop, Cursor, Cline, Windsurf, Zed | [Guide](https://stemsplit.io/en/developers/guides/mcp) |
| [n8n-nodes-stemsplit](https://github.com/StemSplit/n8n-stemsplit) | n8n Community Nodes | n8n community node — stem separation and voice cleaning in workflow automations | [Guide](https://stemsplit.io/en/developers/guides/n8n) |
| [stemsplit-python](https://github.com/StemSplit/stemsplit-python) | `pip install stemsplit-python` | Python SDK for the StemSplit API | [Guide](https://stemsplit.io/en/developers/guides/python) |
| [stemsplit-cli](https://github.com/StemSplit/stemsplit-cli) | `brew install StemSplit/tap/stemsplit` | Command-line tool (Go) — separate stems from the terminal | [Guide](https://stemsplit.io/en/developers/guides/cli) |
| [demucs-onnx](https://github.com/StemSplit/demucs-onnx) | `pip install demucs-onnx` | HTDemucs exported to ONNX — run locally without PyTorch | [API reference](https://stemsplit.io/en/developers/reference) |
| [homebrew-tap](https://github.com/StemSplit/homebrew-tap) | Homebrew tap | Homebrew formulas for StemSplit tools | [Guide](https://stemsplit.io/en/developers/guides/cli) |

## Quick start

**API key** → [stemsplit.io/app/settings/api](https://stemsplit.io/app/settings/api) &nbsp;·&nbsp; **All guides** → [stemsplit.io/en/developers/guides](https://stemsplit.io/en/developers/guides)

```bash
# Separate stems from the CLI
brew install StemSplit/tap/stemsplit
stemsplit separate song.mp3 --output-type BOTH

# Use inside Claude Desktop or Cursor (MCP)
npx -y stemsplit-mcp  # set STEMSPLIT_API_KEY in your MCP config

# Python
pip install stemsplit-python
```

```python
from stemsplit import StemSplitClient

client = StemSplitClient(api_key="sk_live_...")
job = client.separate("song.mp3", output_type="BOTH")
print(job.outputs.vocals_url)
```

## Credits

1 credit = 1 second of audio. New accounts include free credits. [See pricing →](https://stemsplit.io/pricing)
