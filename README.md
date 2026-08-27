<div align="center">
  <h1>XTurnix</h1>
  <p>
    <strong>Streaming dialogue turn prediction based on textual chat history</strong>
  </p>
  <p>
    <a href="https://huggingface.co/xcczach/xturnix-zh-base"><img src="https://img.shields.io/badge/Hugging%20Face-xturnix--zh--base-yellow" alt="Hugging Face model"></a>
    <a href=""><img src="https://img.shields.io/badge/arXiv-Paper-b31b1b" alt="arXiv paper"></a>
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
    <td><a href="https://huggingface.co/xcczach/xturnix-zh-base">XTurnix-ZH Base</a></td>
    <td>A Chinese turn-taking detection model based on large-scale pretraining and general-purpose fine-tuning.</td>
  </tr>
</table>

# Quick Start

Refer to the model repository for instructions. The model has been integrated into the [X-Talk dialogue framework](https://github.com/xcc-zach/xtalk), and you are welcome to try it out.
