<div align="center">
  <h1>XTurnix</h1>
  <p>
    <strong>Streaming dialogue turn prediction based on textual chat history</strong>
  </p>
  <p>
    <a href="https://huggingface.co/xcczach/xturnix-pt"><img src="https://img.shields.io/badge/Hugging%20Face-xturnix--pt-yellow" alt="Hugging Face model"></a>
    <a href="https://huggingface.co/xcczach/xturnix-zh-base"><img src="https://img.shields.io/badge/Hugging%20Face-xturnix--zh--base-yellow" alt="Hugging Face model"></a>
    <a href="https://xtalk.sjtuxlance.com/"><img src="https://img.shields.io/badge/Demo-xtalk-blue" alt="Demo"></a>
    <a href=""><img src="https://img.shields.io/badge/arXiv-Coming%20Soon-b31b1b" alt="arXiv paper coming soon"></a>
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
    <td><a href="https://huggingface.co/xcczach/xturnix-pt">XTurnix Pretrained</a></td>
    <td>A multilingual turn-taking detection model based on large-scale pretraining.</td>
  </tr>
  <tr>
    <td><a href="https://huggingface.co/xcczach/xturnix-zh-base">XTurnix-ZH Base</a></td>
    <td>A Chinese turn-taking detection model built through general-purpose fine-tuning of XTurnix Pretrained.</td>
  </tr>
</table>

# Demo

https://xtalk.sjtuxlance.com/

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
