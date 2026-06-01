# StemSplit

**AI-powered audio stem separation and noise removal — as an API, SDK, CLI, and integrations.**

[stemsplit.io](https://stemsplit.io) &nbsp;·&nbsp; [Developer docs](https://stemsplit.io/en/developers) &nbsp;·&nbsp; [Pricing](https://stemsplit.io/pricing)

---

Separate any song into vocals, drums, bass, piano, guitar, and other stems — or remove background noise from voice recordings — without managing your own ML infrastructure. Powered by [HTDemucs](https://github.com/adefossez/demucs) and [DeepFilterNet](https://github.com/Rikorose/DeepFilterNet) on GPU.

## SDKs & packages

| Package | Install | What it does | Docs |
|---------|---------|--------------|------|
| [node-stemsplit](https://github.com/StemSplit/node-stemsplit) | `npm install @stemsplit/sdk` | **Node.js / TypeScript SDK** — typed client, file uploads, polling helpers, webhooks | [Guide](https://stemsplit.io/en/developers/guides/node) |
| [stemsplit-python](https://github.com/StemSplit/stemsplit-python) | `pip install stemsplit-python` | **Python SDK** — typed Pydantic models, auto file uploads, YouTube jobs | [Guide](https://stemsplit.io/en/developers/guides/python) |
| [stemsplit-mcp](https://github.com/StemSplit/stemsplit-mcp) | `npx -y stemsplit-mcp` | MCP server — stem separation and voice cleaning inside Claude Desktop, Cursor, Cline, Windsurf, Zed | [Guide](https://stemsplit.io/en/developers/guides/mcp) |
| [n8n-nodes-stemsplit](https://github.com/StemSplit/n8n-stemsplit) | n8n Community Nodes | n8n community node — stem separation and voice cleaning in workflow automations | [Guide](https://stemsplit.io/en/developers/guides/n8n) |
| [stemsplit-cli](https://github.com/StemSplit/stemsplit-cli) | `brew install StemSplit/tap/stemsplit` | Command-line tool (Go) — separate stems from the terminal | [Guide](https://stemsplit.io/en/developers/guides/cli) |
| [demucs-onnx](https://github.com/StemSplit/demucs-onnx) | `pip install demucs-onnx` | HTDemucs exported to ONNX — run inference locally without PyTorch | [Docs](https://stemsplit.io/en/developers/reference) |
| [homebrew-tap](https://github.com/StemSplit/homebrew-tap) | Homebrew tap | Homebrew formulas for StemSplit tools | [Guide](https://stemsplit.io/en/developers/guides/cli) |

## Quick start

**API key** → [stemsplit.io/app/settings/api](https://stemsplit.io/app/settings/api) &nbsp;·&nbsp; **All guides** → [stemsplit.io/en/developers/guides](https://stemsplit.io/en/developers/guides)

```bash
# Node.js / TypeScript
npm install @stemsplit/sdk
```

```ts
import { StemSplit } from '@stemsplit/sdk';

const client = new StemSplit(); // reads STEMSPLIT_API_KEY

const job = await client.jobs.create({
  sourceUrl: 'https://example.com/song.mp3',
  outputType: 'FOUR_STEMS',
});
const done = await job.waitForCompletion();
await done.downloadAll('./stems/');
// → stems/vocals.mp3  stems/drums.mp3  stems/bass.mp3  stems/other.mp3
```

```bash
# Python
pip install stemsplit-python
```

```python
from stemsplit_python import StemSplit

client = StemSplit()  # reads STEMSPLIT_API_KEY
job = client.jobs.create(source_url="https://example.com/song.mp3", output_type="BOTH").wait()
job.download_all("./out/")
```

```bash
# CLI
brew install StemSplit/tap/stemsplit
stemsplit separate song.mp3 --output-type BOTH

# AI assistants (Claude Desktop, Cursor, Cline…)
npx -y stemsplit-mcp  # set STEMSPLIT_API_KEY in your MCP config
```

## Credits

1 credit = 1 second of audio. New accounts include free credits. [See pricing →](https://stemsplit.io/pricing)
