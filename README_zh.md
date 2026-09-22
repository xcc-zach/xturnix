<div align="center">
  <h1>XTurnix</h1>
  <p>
    <strong>基于文本聊天历史的流式对话话轮预测</strong>
  </p>
  <p>
    <a href="https://huggingface.co/xcczach/xturnix-pt"><img src="https://img.shields.io/badge/Hugging%20Face-xturnix--pt-yellow" alt="Hugging Face 模型"></a>
    <a href="https://huggingface.co/xcczach/xturnix-zh-base"><img src="https://img.shields.io/badge/Hugging%20Face-xturnix--zh--base-yellow" alt="Hugging Face 模型"></a>
    <a href="https://xtalk.sjtuxlance.com/"><img src="https://img.shields.io/badge/Demo-xtalk-blue" alt="Demo"></a>
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

# Demo

https://xtalk.sjtuxlance.com/

# 模型

<table>
  <tr>
    <td><a href="https://huggingface.co/xcczach/xturnix-pt">XTurnix Pretrained</a></td>
    <td>基于大规模预训练的多语言话轮检测模型</td>
  </tr>
  <tr>
    <td><a href="https://huggingface.co/xcczach/xturnix-zh-base">XTurnix-ZH Base</a></td>
    <td>基于XTurnix Pretrained通用微调的中文话轮检测模型</td>
  </tr>
</table>

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
