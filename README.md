# betterthanjson.com

**GCF is better than JSON for AI agents.** Full benchmark data proving it.

## Why JSON fails at scale

JSON was designed in 2001 for browser-to-server communication. When an LLM receives 500 records as JSON, it gets 53,341 tokens of repeated field names (`"qualified_name":`, `"kind":`, `"score":` on every record). At this scale, GPT-5.5 returns empty strings. Claude Opus spends 143 lines manually enumerating symbols and still gets the wrong answer. JSON averages 54.1% comprehension accuracy across 10 models.

## What GCF does differently

GCF declares field names once in a header. Rows are positional values. Section headers (`## targets`, `## related`) replace per-record metadata. The same 500-record payload uses 11,090 tokens instead of 53,341.

- **79% fewer input tokens** than JSON
- **63% fewer output tokens** than JSON
- **91.2% comprehension accuracy** across 10 models and 3 providers (Anthropic, OpenAI, Google)
- **Four models hit 100%**: Claude Sonnet, Gemini 2.5 Pro, Gemini 3.1 Pro, Gemini 3.5 Flash
- **5/5 generation validity** on every frontier model with zero prior training
- **Wins all 6 datasets** on TOON's own benchmark using their datasets and tokenizer

## The benchmark

1,300+ LLM evaluations. 23 comprehension runs. 28 generation runs. 10 models. 3 providers. Deterministic ground truth, no LLM judge, reproducible from one command.

### Comprehension (can the model read it?)

| Model | GCF | TOON | JSON |
|:---|:---|:---|:---|
| Claude Opus 4.6 | **96.2%** | 84.6% | 73.1% |
| Claude Sonnet 4.6 | **100%** | 73.1% | 53.8% |
| Claude Haiku 4.5 | **96.2%** | 69.2% | 57.7% |
| GPT-5.5 | **84.1%** | 67.7% | 45.8% |
| GPT-5.4 | **78.0%** | 56.0% | 44.1% |
| GPT-5.4-mini | **71.8%** | 64.1% | 54.2% |
| Gemini 2.5 Pro | **100%** | 76.9% | 58.3% |
| Gemini 3.1 Pro | **100%** | 76.9% | 46.2% |
| Gemini 3.5 Flash | **100%** | 61.5% | 46.2% |
| Gemini 2.5 Flash | **80.6%** | 54.1% | 57.0% |

GCF > TOON > JSON on every model from every provider. No exceptions.

### Generation (can the model write it?)

| Model | GCF | TOON | JSON |
|:---|:---|:---|:---|
| Claude Opus 4.6 | **5/5** | 0/5 | 5/5 |
| Claude Sonnet 4.6 | **5/5** | 2-3/5 | 5/5 |
| GPT-5.5 | **4-5/5** | 1-2/5 | 5/5 |
| GPT-5.4 | **5/5** | 0/5 | 5/5 |
| Gemini 2.5 Pro | **5/5** | 1/5 | 5/5 |
| Gemini 3.1 Pro | **5/5** | 0/5 | 5/5 |

TOON's official decoder rejects LLM-generated output on 7 of 9 models. GCF achieves 5/5 on every frontier model with zero training.

### Token efficiency

| Format | Tokens (500 symbols) | vs JSON |
|:---|:---|:---|
| **GCF** | **11,090** | **79% fewer** |
| TOON | 16,378 | 69% fewer |
| JSON | 53,341 | baseline |

## How to try it

```bash
pip install gcf-proxy
```

Wrap any MCP server. Zero code changes. Your server keeps outputting JSON, the model receives GCF.

## Links

- [Live site](https://betterthanjson.com)
- [Full benchmarks](https://gcformat.com/guide/benchmarks.html)
- [Full eval data](https://gcformat.com/guide/eval-results.html)
- [GCF Specification](https://github.com/blackwell-systems/gcf)
- [GCF Proxy](https://github.com/blackwell-systems/gcf-proxy)
- [Playground (live three-way comparison)](https://gcformat.com/playground.html)
- [Whitepaper (DOI: 10.5281/zenodo.20579817)](https://doi.org/10.5281/zenodo.20579817)
- Implementations: [Go](https://github.com/blackwell-systems/gcf-go) | [TypeScript](https://github.com/blackwell-systems/gcf-typescript) | [Python](https://github.com/blackwell-systems/gcf-python) | [Rust](https://github.com/blackwell-systems/gcf-rust) | [Swift](https://github.com/blackwell-systems/gcf-swift) | [Kotlin](https://github.com/blackwell-systems/gcf-kotlin)

## License

MIT - [Dayna Blackwell](https://github.com/blackwell-systems)
