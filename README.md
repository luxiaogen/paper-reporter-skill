# 论文汇报助手 (Paper Reporter Skill)

> 🎓 专为学术组会、答辩及论文研讨打造的 AI Agent 结构化论文汇报引导技能包。

`paper-reporter` 是一个用于 Agent（如 Google Antigravity / Agentic Coding Assistant）的专属 Skill。它能够引导用户按照精细设计的 **9 步逻辑框架** 逐步拆解和梳理学术论文，确保最终的汇报大纲条理清晰、重点突出、逻辑严密，并深度理解模型/算法模块与其解决的具体问题之间的映射关联。

---

## 🌟 核心特性 (Features)

- **强关联映射**：强制要求每个提出的模型/算法模块都清晰绑定其所解决的具体问题。
- **合理推演机制**：当论文原文未明确说明设计初衷时，引导用户基于第一性原理与领域知识进行合理补充。
- **总-分结构分析**：先看宏观架构与流水线，再深入拆解子模块设计与公式原理。
- **批判性思维**：引导分析实验消融结果、超参敏感性以及论文可能的逻辑漏洞与局限。
- **一键大纲导出**：梳理完成后自动生成结构化的汇报大纲，支持 Markdown / Google Docs 等格式存档。

---

## 📦 安装教程 (Installation)

### 方法一：🤖 给 AI Agent 的一键自动安装（推荐直接发送给 Agent）

只需复制以下提示词发送给你的 AI Agent（如 Antigravity / Agentic Coding Assistant），Agent 将自动打开终端进行克隆与配置：

> 💬 **发送给 Agent 的提示词：**  
> *"请帮我在本地安装 `paper-reporter` skill，仓库地址为：https://github.com/luxiaogen/paper-reporter-skill.git 。请在终端中运行以下命令完成安装："*  
> ```bash
> mkdir -p ~/.gemini/config/skills && cd ~/.gemini/config/skills && git clone https://github.com/luxiaogen/paper-reporter-skill.git paper-reporter
> ```

---

### 方法二：手动 Clone 到个人 Skill 配置目录

打开终端，直接将本仓库克隆至你的 Antigravity Skill 全局配置目录下：

```bash
mkdir -p ~/.gemini/config/skills
cd ~/.gemini/config/skills
git clone https://github.com/luxiaogen/paper-reporter-skill.git paper-reporter
```

---

### 方法三：手动下载配置文件

1. 下载本仓库中的 [SKILL.md](https://raw.githubusercontent.com/luxiaogen/paper-reporter-skill/main/SKILL.md) 配置文件。
2. 在你的配置路径 `~/.gemini/config/skills/` 下新建 `paper-reporter` 文件夹。
3. 将 `SKILL.md` 放入该文件夹中即可。

---

## 🚀 使用方法与触发词 (Usage)

安装完成后，在与 Agent 对话时，只需提及以下任意关键词即可自动触发“论文汇报助手”技能：

- “帮我梳理这篇论文，准备组会汇报”
- “论文汇报助手”
- “梳理论文” / “论文讲解”
- “组会汇报大纲” / “paper report”

---

## 📋 9 步引导工作流 (9-Step Workflow)

| 步骤 | 阶段 | 引导重点与策略 |
|---|---|---|
| **步骤 1** | 摘要与整体方案 | 明确论文针对的具体问题、包含的核心模块及具体功能。 |
| **步骤 2** | 导言 (Introduction) | 厘清背景、现有工作、具体问题（必须具体）、问题后果及解决思路。 |
| **步骤 3** | 相关工作 (Related Work) | **跳过**，集中精力于本文创新点。 |
| **步骤 4** | 方法与正文 (Method) | 采用“总-分”结构，先整体拓扑后子模块拆解，强制解释设计原因与解决的问题。 |
| **步骤 5** | 关键公式与算法 | 解释核心公式原理，必要时举例推导（如匹配/注意力过程）。 |
| **步骤 6** | 实验 (Experiments) | 分析主实验、消融实验、超参效果，定位效果最好的组件及原因。 |
| **步骤 7** | 批判性思考 | 主动寻找论文的局限性、未解释现象或逻辑漏洞。 |
| **步骤 8** | 结论 (Conclusion) | 一句话带过或略过。 |
| **步骤 9** | 最终汇报整理 | 汇总生成结构化汇报大纲并存档。 |

---

## 💡 汇报大纲输出示例 (Example Output)

完成引导讨论后，助手将生成如下结构的汇报大纲：

# 【组会汇报大纲】论文名称 / 主题

## 1. 核心问题与解决方案 (Core Problem & Solution)
- **核心问题**：现有模型在遮挡场景下特征易丢失、匹配鲁棒性差。
- **总体方案**：提出了包含遮挡感知注意力 (OAM) 与双向匈牙利匹配 (BHM) 的端到端目标检测框架。

## 2. 背景与问题切入 (Introduction)
- **具体痛点**：轻度遮挡即导致边界框漂移（定位精度下降 15%）。
- **解决思路**：引入时序上下文与空间掩码，显式建模遮挡区域特征。

## 3. 方法与架构拆解 (Methodology)
- **总体架构**：Backbone -> OAM 模块 -> BHM 匹配头 -> Loss 计算。
- **关键模块 1 - 遮挡感知注意力 (OAM)**：
  - *设计初衷*：抑止掩码区域的高频噪声。
  - *具体解决*：降低遮挡像素在特征图上的权重。
- **关键公式原理**：
  $$\mathcal{L}_{OAM} = -\sum y \log(\sigma(W \cdot F))$$

## 4. 实验结果与消融分析 (Experiments)
- **最佳组件**：OAM 模块带来最大的性能提升（+4.2% mAP）。
- **超参敏感度**：掩码阈值 $\tau=0.5$ 时性能达到顶峰。

## 5. 批判性思考与讨论 (Critical Thinking)
- **局限性**：在大面积严重遮挡（>80%）时推理延迟大幅增加。
- **未来方向**：轻量化掩码预测分支。

---

## 📄 开源协议 (License)

[MIT License](LICENSE)
