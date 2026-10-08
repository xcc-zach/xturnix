<div align="center">
  <h1>XTurnix</h1>
  <p>
    <strong>基于文本聊天历史的流式对话话轮预测模型</strong>
  </p>
  <p>
    <a href="https://huggingface.co/xcczach/xturnix-pt"><img src="https://img.shields.io/badge/Hugging%20Face-xturnix--pt-yellow" alt="Hugging Face 模型"></a>
    <a href="https://huggingface.co/xcczach/xturnix-zh-base"><img src="https://img.shields.io/badge/Hugging%20Face-xturnix--zh--base-yellow" alt="Hugging Face 模型"></a>
    <a href="https://huggingface.co/spaces/xcczach/xturnix-demo"><img src="https://img.shields.io/badge/Hugging%20Face%20Spaces-Demo-yellow" alt="Hugging Face 演示"></a>
    <a href="https://xtalk.sjtuxlance.com/"><img src="https://img.shields.io/badge/Demo-xtalk-blue" alt="Demo"></a>
    <a href="https://arxiv.org/abs/2610.04400"><img src="https://img.shields.io/badge/arXiv-paper-b31b1b" alt="arXiv 论文"></a>
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

# Demo

[Hugging Face Demo](https://huggingface.co/spaces/xcczach/xturnix-demo)

[对话系统集成](https://xtalk.sjtuxlance.com/)

# 模型

<table>
  <tr>
    <td><a href="https://huggingface.co/xcczach/xturnix-pt">XTurnix Pretrained 0.6B</a></td>
    <td>基于大规模预训练的多语言话轮检测模型</td>
  </tr>
  <tr>
    <td><a href="https://huggingface.co/xcczach/xturnix-zh-base">XTurnix-ZH Base 0.6B</a></td>
    <td>基于XTurnix Pretrained通用微调的中文话轮检测模型</td>
  </tr>
</table>

# Benchmark Results

中文（ZH）和英文（EN）上的准确率（%）。最优结果加粗，次优结果用斜体。

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

# 快速开始

参考 Hugging Face 模型仓库中的说明使用`vllm`部署模型。该模型已集成到 [X-Talk 对话框架](https://github.com/xcc-zach/xtalk) 中，可参见 [X-Talk 快速开始](https://xtalk.readthedocs.io/zh/quickstart/)、[X-Talk 配置](https://xtalk.readthedocs.io/zh/tutorial/config_the_service/) 与 [支持的模型](https://xtalk.readthedocs.io/zh/technical_reference/supported_models/#_5) 获取指引。如需连接由 `vllm` 部署在 8000 端口的模型，配置项应如下所示：
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
