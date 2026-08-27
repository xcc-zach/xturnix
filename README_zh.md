<div align="center">
  <h1>XTurnix</h1>
  <p>
    <strong>基于文本聊天历史的流式对话话轮预测</strong>
  </p>
  <p>
    <a href="https://huggingface.co/xcczach/xturnix-zh-base"><img src="https://img.shields.io/badge/Hugging%20Face-xturnix--zh--base-yellow" alt="Hugging Face 模型"></a>
    <a href=""><img src="https://img.shields.io/badge/arXiv-Paper-b31b1b" alt="arXiv 论文"></a>
    <a href="LICENSE"><img src="https://img.shields.io/badge/License-Apache%202.0-green" alt="Apache-2.0"></a>
  </p>
</div>

[English](README.md) | [中文](README_zh.md)

根据转写后的对话历史预测话轮决策：当 AI 正在聆听时，判断它应该继续聆听还是开始说话；当用户在 AI 说话期间发言时，判断 AI 应该继续说话还是停止说话并转为聆听。

模型会维护 AI 的当前状态，并在每次收到用户输入时作出话轮决策：

| 当前 AI 状态 | XTurnix 决策 | XTurnix 输出 |
| --- | --- | --- |
| `listening` | 用户尚未结束当前话轮，继续聆听 | `keep` |
| `listening` | 用户已经结束当前话轮，开始回复 | `start` |
| `speaking` | 用户输入不要求 AI 让出当前话轮 | `keep` |
| `speaking` | 用户输入要求 AI 停止说话并转为聆听 | `stop` |

# 模型

<table>
  <tr>
    <td><a href="https://huggingface.co/xcczach/xturnix-zh-base">XTurnix-ZH Base</a></td>
    <td>基于大规模预训练和通用微调的中文话轮检测模型</td>
  </tr>
</table>

# 快速开始

参考模型仓库。模型已在[X-Talk对话框架](https://github.com/xcc-zach/xtalk)中适配，欢迎体验。
