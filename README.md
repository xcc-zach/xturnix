<div align="center">
  <h1>XTurnix</h1>
  <p>
    <strong>Streaming dialogue turn prediction model based on textual chat history</strong>
  </p>
  <p>
    <a href="https://huggingface.co/xcczach/xturnix-pt"><img src="https://img.shields.io/badge/Hugging%20Face-xturnix--pt-yellow" alt="Hugging Face model"></a>
    <a href="https://huggingface.co/xcczach/xturnix-zh-base"><img src="https://img.shields.io/badge/Hugging%20Face-xturnix--zh--base-yellow" alt="Hugging Face model"></a>
    <a href="https://huggingface.co/spaces/xcczach/xturnix-demo"><img src="https://img.shields.io/badge/Hugging%20Face%20Spaces-Demo-yellow" alt="Hugging Face demo"></a>
    <a href="https://xtalk.sjtuxlance.com/"><img src="https://img.shields.io/badge/Demo-xtalk-blue" alt="Demo"></a>
    <a href="https://arxiv.org/abs/2610.04400"><img src="https://img.shields.io/badge/arXiv-paper-b31b1b" alt="arXiv paper"></a>
    <a href="LICENSE"><img src="https://img.shields.io/badge/License-Apache%202.0-green" alt="Apache-2.0"></a>
  </p>
</div>

[English](README.md) | [中文](README_zh.md)

Predict turn-taking decisions from transcribed dialogue history: whether the AI should keep listening or start speaking while listening, and whether it should keep speaking or stop and listen when the user speaks while the AI is speaking.

The model maintains the AI's current state and makes a turn-taking decision whenever it receives user input:

| Current AI state | XTurnix decision | XTurnix output |
| --- | --- | --- |
| `listening` | The user has not finished the current turn; keep listening | `keep` |
| `listening` | The user has finished the current turn; start responding | `start` |
| `speaking` | The user input does not require the AI to yield the current turn | `keep` |
| `speaking` | The user input requires the AI to stop speaking and listen | `stop` |

# Models

<table>
  <tr>
    <td><a href="https://huggingface.co/xcczach/xturnix-pt">XTurnix Pretrained 0.6B</a></td>
    <td>A multilingual turn-taking detection model based on large-scale pretraining.</td>
  </tr>
  <tr>
    <td><a href="https://huggingface.co/xcczach/xturnix-zh-base">XTurnix-ZH Base 0.6B</a></td>
    <td>A Chinese turn-taking detection model built through general-purpose fine-tuning of XTurnix Pretrained.</td>
  </tr>
</table>

# Demo

[Huggingface Demo](https://huggingface.co/spaces/xcczach/xturnix-demo)

[Dialogue System Integration](https://xtalk.sjtuxlance.com/)

# Benchmark Results

Accuracy(%) on Chinese (ZH) and English (EN). Best results are bold, and second-best
italicized.

| Model | Params | Easy-Turn ZH | Smart-Turn All | Smart-Turn ZH | Smart-Turn EN | SemanticVAD All | SemanticVAD ZH | SemanticVAD EN | LiveKit All | LiveKit ZH | LiveKit EN |
|-------|--------|-------------:|---------------:|--------------:|--------------:|----------------:|---------------:|---------------:|------------:|-----------:|-----------:|
| Easy-Turn | 850M | **97.33** | -- | 13.31 | -- | -- | 70.06 | -- | -- | 55.45 | -- |
| Smart-Turn | 8M | 77.17 | *98.81* | **98.52** | 99.00 | 54.61 | 53.09 | 69.75 | *70.91* | 64.60 | *76.24* |
| FireRedChat | 170M | 81.17 | 9.29 | 1.78 | 14.34 | 72.42 | 72.59 | 70.75 | 42.67 | 42.91 | 42.48 |
| Namo | 307M | 50.83 | 44.17 | 48.52 | 41.24 | 46.14 | 45.68 | 50.75 | 49.92 | 44.20 | 54.75 |
| TEN | 7B | 90.33 | 74.40 | 74.85 | 74.10 | 62.65 | 61.14 | 77.75 | 63.50 | 61.20 | 65.45 |
| TurnSense | 47M | *96.17* | 79.40 | 94.97 | 68.92 | 64.86 | 64.32 | 70.25 | 58.08 | 58.73 | 57.52 |
| SoulX-Duplug | 0.6B | 64.83 | 94.52 | 92.31 | 96.02 | 72.69 | 74.02 | 59.50 | 61.67 | 58.85 | 64.06 |
| X2-Turn | 4B | 76.50 | 98.57 | *97.04* | **99.60** | 80.66 | 80.88 | *78.50* | 64.79 | 59.79 | 69.01 |
| Qwen3-0.6B | 0.6B | 49.50 | 0.00 | 0.00 | 0.00 | 38.33 | 37.76 | 44.00 | 43.05 | 40.45 | 45.25 |
| Synthetic-only | 0.6B | 55.67 | 94.05 | 90.24 | 96.61 | 65.97 | 66.85 | 57.00 | 53.52 | 53.58 | 53.47 |
| XTurnix-PT | 0.6B | 86.00 | **98.93** | **98.52** | *99.20* | *84.08* | *84.97* | 75.25 | **73.70** | **70.57** | **76.34** |
| XTurnix-ZH-Base | 0.6B | 95.33 | 97.38 | 96.75 | 97.81 | **92.14** | **93.36** | **80.00** | *70.91* | *66.47* | 74.65 |



# Quickstart

Refer to the Huggingface model repositories for instructions to deploy with `vllm`. The model has been integrated into the [X-Talk dialogue framework](https://github.com/xcc-zach/xtalk), and see [X-Talk quickstart](https://xtalk.readthedocs.io/quickstart/), [X-Talk configuration](https://xtalk.readthedocs.io/tutorial/config_the_service/) and [Supported Models](https://xtalk.readthedocs.io/technical_reference/supported_models/#turn-detection) for guidance. To connect to model deployed by `vllm` on port 8000, the config item should be like:
```json
 {
  "turn_detector": {
    "type": "XTurnix",
    "params": {
      "base_url": "http://127.0.0.1:8000",
      "timeout": 2.0,
      "max_model_len": 2048
    }
  }
}
```
