<p align="center">
  <a href="https://stemsplit.io">
    <img src="https://stemsplit.io/icon.svg" alt="StemSplit" width="80" height="80" />
  </a>
</p>

<h1 align="center">StemSplit</h1>

<p align="center">
  <strong>AI-powered stem separation and voice cleaning — API, SDKs, CLI, and open-source ONNX inference.</strong>
</p>

<p align="center">
  <a href="https://stemsplit.io">Website</a> &nbsp;·&nbsp;
  <a href="https://stemsplit.io/developers">Developer docs</a> &nbsp;·&nbsp;
  <a href="https://stemsplit.io/app/settings/api">API keys</a> &nbsp;·&nbsp;
  <a href="https://stemsplit.io/pricing">Pricing</a> &nbsp;·&nbsp;
  <a href="https://stemsplit.io/free-trial">Free trial</a>
</p>

<p align="center">
  <a href="https://pypi.org/project/demucs-onnx"><img src="https://img.shields.io/pypi/v/demucs-onnx?label=demucs-onnx" alt="PyPI demucs-onnx" /></a>
  <a href="https://pypi.org/project/stemsplit-python"><img src="https://img.shields.io/pypi/v/stemsplit-python?label=stemsplit-python" alt="PyPI stemsplit-python" /></a>
  <a href="https://www.npmjs.com/package/@stemsplit/sdk"><img src="https://img.shields.io/npm/v/@stemsplit/sdk?label=%40stemsplit%2Fsdk" alt="npm @stemsplit/sdk" /></a>
  <a href="https://github.com/StemSplit/demucs-onnx/blob/main/LICENSE"><img src="https://img.shields.io/github/license/StemSplit/demucs-onnx" alt="License MIT" /></a>
</p>

---

Separate any song into **vocals, drums, bass, piano, guitar, and other** stems — or **clean voice recordings** (noise, hum, echo) — without running your own GPU fleet. Models are based on [HTDemucs](https://github.com/adefossez/demucs) and [DeepFilterNet](https://github.com/Rikorose/DeepFilterNet). Use our [hosted API](https://stemsplit.io/developers) or run the same lineage **locally** with [demucs-onnx](https://github.com/StemSplit/demucs-onnx).

## Choose your path

| I want to… | Start here |
|------------|------------|
| **Call the API from code** | [node-stemsplit](https://github.com/StemSplit/node-stemsplit) (`npm i @stemsplit/sdk`) · [stemsplit-python](https://github.com/StemSplit/stemsplit-python) (`pip install stemsplit-python`) |
| **Run separation locally** (no PyTorch) | [demucs-onnx](https://github.com/StemSplit/demucs-onnx) · [ONNX models on Hugging Face](https://huggingface.co/StemSplitio) · [browser guide](https://stemsplit.github.io/demucs-onnx/browser/) |
| **Automate in CI/CD** | [stemsplit-github-action](https://github.com/StemSplit/stemsplit-github-action) |
| **No-code & AI agents** | [n8n-stemsplit](https://github.com/StemSplit/n8n-stemsplit) · [stemsplit-mcp](https://github.com/StemSplit/stemsplit-mcp) · [zapier-stemsplit](https://github.com/StemSplit/zapier-stemsplit) |
| **Terminal / scripts** | [stemsplit-cli](https://github.com/StemSplit/stemsplit-cli) — `brew install StemSplit/tap/stemsplit` ([homebrew-tap](https://github.com/StemSplit/homebrew-tap)) |

## Run locally (open source)

[**demucs-onnx**](https://github.com/StemSplit/demucs-onnx) exports HTDemucs FT to ONNX and runs inference with **numpy + onnxruntime** only — Python CLI, browser (`onnxruntime-web`), and mobile-friendly weights on [Hugging Face](https://huggingface.co/StemSplitio).

```bash
pip install 'demucs-onnx[mp3]'
demucs-onnx separate song.mp3 out/ --karaoke --mp3
```

- **Docs:** [stemsplit.github.io/demucs-onnx](https://stemsplit.github.io/demucs-onnx/)
- **Benchmark dataset:** [StemSplitio/stem-separation-benchmark-2026](https://huggingface.co/datasets/StemSplitio/stem-separation-benchmark-2026) — SDR, RTF, and hardware notes
- **Prefer hosted inference?** Same model family on GPU via the [StemSplit API](https://stemsplit.io/developers) — pay per second of audio.

## Hosted API — quick start

Get an API key at [stemsplit.io/app/settings/api](https://stemsplit.io/app/settings/api). Set `STEMSPLIT_API_KEY` in your environment. Full guides: [stemsplit.io/developers/guides](https://stemsplit.io/developers/guides).

**Node.js / TypeScript** — [`@stemsplit/sdk`](https://www.npmjs.com/package/@stemsplit/sdk) · [guide](https://stemsplit.io/developers/guides/node)

```bash
npm install @stemsplit/sdk
export STEMSPLIT_API_KEY=your_key_here
```

```ts
import { StemSplit } from "@stemsplit/sdk";

const client = new StemSplit();
const job = await client.jobs.create({
  sourceUrl: "https://example.com/song.mp3",
  outputType: "FOUR_STEMS",
});
const done = await job.waitForCompletion();
await done.downloadAll("./stems/");
```

**Python** — [`stemsplit-python`](https://pypi.org/project/stemsplit-python/) · [guide](https://stemsplit.io/developers/guides/python)

```bash
pip install stemsplit-python
export STEMSPLIT_API_KEY=your_key_here
```

```python
from stemsplit_python import StemSplit

client = StemSplit()
job = client.jobs.create(
    source_url="https://example.com/song.mp3",
    output_type="BOTH",
).wait()
job.download_all("./out/")
```

**CLI** — [guide](https://stemsplit.io/developers/guides/cli)

```bash
brew install StemSplit/tap/stemsplit
export STEMSPLIT_API_KEY=your_key_here
stemsplit separate song.mp3 --output-type BOTH
```

## Integrations

| Project | Install / use | Docs |
|---------|---------------|------|
| [stemsplit-mcp](https://github.com/StemSplit/stemsplit-mcp) | `npx -y stemsplit-mcp` | [MCP guide](https://stemsplit.io/developers/guides/mcp) |
| [n8n-stemsplit](https://github.com/StemSplit/n8n-stemsplit) | n8n Community Nodes (`n8n-nodes-stemsplit`) | [n8n guide](https://stemsplit.io/developers/guides/n8n) |
| [zapier-stemsplit](https://github.com/StemSplit/zapier-stemsplit) | Zapier StemSplit integration | [Zapier guide](https://stemsplit.io/developers/guides/zapier) |
| [stemsplit-github-action](https://github.com/StemSplit/stemsplit-github-action) | `uses: StemSplit/stemsplit-github-action@v0.1.0` | [GitHub Actions guide](https://stemsplit.io/developers/guides/github-actions) |

**MCP (Cursor, Claude Desktop, Cline, …):** add `stemsplit-mcp` to your MCP config with `STEMSPLIT_API_KEY` — see the [MCP setup guide](https://stemsplit.io/developers/guides/mcp).

## Models & research

| Resource | Link |
|----------|------|
| Hugging Face org | [huggingface.co/StemSplitio](https://huggingface.co/StemSplitio) — ONNX + PyTorch model repos |
| Benchmark dataset | [stem-separation-benchmark-2026](https://huggingface.co/datasets/StemSplitio/stem-separation-benchmark-2026) |
| API reference | [stemsplit.io/developers/reference](https://stemsplit.io/developers/reference) |

```bibtex
@misc{stemsplit_benchmark_2026,
  title  = {StemSplit Stem-Separation Benchmark 2026},
  author = {StemSplit},
  year   = {2026},
  url    = {https://huggingface.co/datasets/StemSplitio/stem-separation-benchmark-2026}
}
```

## Community

- **Questions & ideas:** [GitHub Discussions on demucs-onnx](https://github.com/StemSplit/demucs-onnx/discussions)
- **Bugs:** open an issue on the repo you are using (start with [demucs-onnx issues](https://github.com/StemSplit/demucs-onnx/issues) for local inference)
- **Contributing:** see [CONTRIBUTING.md](https://github.com/StemSplit/demucs-onnx/blob/main/CONTRIBUTING.md) on `demucs-onnx` and sibling repos
- **Updates:** [@StemSplit on X](https://x.com/StemSplit)

## Credits & pricing

**1 credit = 1 second of audio processed.** New accounts include **free credits** to try the API and integrations. See [pricing](https://stemsplit.io/pricing) and [free trial](https://stemsplit.io/free-trial).
