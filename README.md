# GRE Verbal Analysis

AI 驱动的 GRE Verbal 模考深度解析工具。自动抓取模考结果，逐题生成包含逻辑解析、词汇拆解、错误诊断的完整分析报告。

基于 [WorkBuddy Skill](https://www.codebuddy.cn) 架构，也可在任意 AI 平台上使用。

---

## 你有没有这些痛点？

- 📕 **刷题网解析不全** — 只给答案，不讲解题逻辑
- ✂️ **需要逐题截图/复制搜题** — 一题一题去搜，太慢了
- 🔄 **频繁切换页面/题号效率低下** — 在模考平台和解析网站之间来回切
- 📉 **搜题生成的解析质量不稳定** — 有的讲得清楚，有的根本没讲
- ⚙️ **需要多次调整提示词达到想要的效果** — 每次都要重新教 AI 怎么分析

**这个工具一次性解决以上所有问题。**

---

## 快速开始（3 分钟上手）

### 如果你是考生（想分析自己的模考）

**输入**：你的 GRE 模考结果页面 URL（目前支持 gre.viplgw.cn，其他平台可手动输入题目）

**输出**：一份完整的解析报告，包含：
- 📊 分数总览与能力雷达图
- 📝 逐题深度解析（每题 5 个模块）
- 📚 词汇记忆卡片（含词根 + 记忆技巧）
- 🧠 方法论总结（建立你的答题体系）

**怎么做**：
1. 考完模考，复制结果页面 URL
2. 打开 WorkBuddy，说："帮我分析这份 GRE Verbal 模考"
3. 粘贴 URL，等待 2-3 分钟
4. 收到 `GRE_Verbal_解析报告.html`，用浏览器打开即可查看

---

## 输入格式（三种方式）

| 方式 | 格式 | 说明 |
|------|------|------|
| **方式 1：URL**（推荐） | `https://gre.viplgw.cn/mockResult/...` | 自动抓取，最方便 |
| **方式 2：手动输入题目** | 纯文本，直接粘贴题目 | 无需浏览器自动化 |
| **方式 3：JSON 数据** | 见 `skill/references/data_schema.json` | 适合程序化调用 |

> **支持的平台**：目前浏览器自动化仅支持 gre.viplgw.cn（雷哥GRE）。其他平台（考满分、微臣等）可以手动粘贴题目文本，同样能生成完整解析。

---

## 输出内容（每题 5 个解析模块）

1. **句子逻辑拆解** — 分析句子结构、逻辑方向（正/负）、关键词定位
2. **选项逐一讲解** — 不只讲正确答案，所有干扰项都分析为什么错
3. **核心词汇注解** — 高频词 + 词根 + 记忆技巧（不是死记硬背）
4. **错误诊断** — 如果做错了，归类错误类型（词汇盲区 / 逻辑方向反了 / 形近词混淆等）
5. **方法论总结** — 这类题的标准解题流程，下次遇到怎么做

---

## 功能特性

- **全部 24 题逐题解析**：Section 1（11 题）+ Section 3（13 题）
- **做对的题也分析** — 捕捉"蒙对"的情况
- **双格式报告**：HTML（精美排版，可打印）+ Markdown（纯文本，方便编辑）
- **响应式设计**：手机/平板/电脑都能看
- **可复用知识库**：高频词汇表、SE 同义词簇、RC 题型策略

---

## 项目结构

```
gre-verbal-analysis/
├── README.md                    # 本文件
├── LICENSE                      # MIT 开源协议
├── .gitignore
├── skill/
│   ├── SKILL.md                 # WorkBuddy Skill 定义（4 阶段工作流）
│   ├── SYSTEM_PROMPT.md         # 通用 Prompt（可用于任意 AI 平台）
│   ├── scripts/                 # （预留）自动化脚本
│   ├── references/
│   │   ├── gre_high_freq_words.md       # GRE 高频词汇表
│   │   ├── se_synonym_clusters.md       # SE 同义词对聚类
│   │   ├── rc_question_types.md         # RC 题型策略
│   │   └── data_schema.json             # 输入数据 JSON Schema
│   └── assets/
│       └── report_template.html         # HTML 报告模板
└── samples/
    └── sample_report.html       # 示例报告（匿名化）
```

---

## 在 WorkBuddy 上使用

1. 将 `skill/` 目录复制到 `~/.workbuddy/skills/gre-verbal-analysis/`
2. 对 WorkBuddy 说：**"帮我分析 GRE Verbal 模考"**
3. 粘贴你的模考结果 URL（gre.viplgw.cn）
4. 确保浏览器已开启调试端口（见下方"浏览器配置"）

### 浏览器配置（仅 URL 方式需要）

如果用的是 URL 自动抓取方式，需要让浏览器开启调试端口：

```bash
# Chrome
chrome --remote-debugging-port=9222

# Edge
msedge --remote-debugging-port=9222
```

---

## 在 Claude / OpenClaw / 任意 AI 平台上使用

核心解析逻辑（Phase 2/3）完全平台无关，不依赖 WorkBuddy。

**步骤**：
1. 打开你的 AI 平台（Claude、OpenClaw、ChatGPT 等）
2. 将 `skill/SYSTEM_PROMPT.md` 的内容作为 **System Prompt** 粘贴进去
3. 提供题目数据（URL / 手动输入 / JSON 均可）
4. AI 会按照同样的标准输出完整解析报告

---

## 题型支持

| 题型代码 | 全称 | 格式 |
|---------|------|------|
| **SC** | Single Choice | 单空，5 选 1 |
| **SE** | Sentence Equivalence | 单空，6 选 2（两个同义词） |
| **TC2** | Text Completion (2 blanks) | 两空，每组多选 |
| **TC3** | Text Completion (3 blanks) | 三空，每组多选 |
| **RC** | Reading Comprehension | 阅读理解，含多种子题型 |

---

## 错误类型分类

系统会将每道错题归类，帮助你发现规律：

| 错误类型 | 说明 |
|---------|------|
| Vocabulary gap | 关键词不认识 |
| Wrong logic direction | 逻辑方向搞反（正/负） |
| Look-alike confusion | 形近词混淆（如 comely vs comic） |
| Unsupported inference | RC 细节题做了无根据的推断 |
| Speed error | 做得太快，大概率是蒙的 |
| Blank answer | 空着没选，白白丢分 |
| Non-synonymous SE pair | SE 选了两个不是同义词的选项 |
| Reversed "unlike" logic | "unlike" 类题目逻辑方向反了 |

---

## 示例报告

查看 [`samples/sample_report.html`](samples/sample_report.html) 了解报告的实际效果。

---

## 技术栈

- **AI 工作流**：WorkBuddy Skill（LLM 驱动的多阶段流程）
- **浏览器自动化**：CDP（Chrome DevTools Protocol）
- **输出格式**：静态 HTML + Markdown（无需服务器）
- **样式**：纯 CSS 变量，响应式设计

---

## 常见问题

**Q：只能用于 gre.viplgw.cn 吗？**
A：浏览器自动抓取目前只支持 gre.viplgw.cn。但你可以手动粘贴任何平台的题目文本，解析质量完全相同。

**Q：报告是中文还是英文？**
A：报告以中文为主，方便中国考生阅读。题目原文和词汇保持英文。

**Q：需要联网吗？**
A：首次抓取需要联网访问模考平台。生成解析报告本身不需要联网。

**Q：我的模考数据会被上传吗？**
A：如果你使用 WorkBuddy 本地版本，所有数据只在本地处理，不会上传。

---

## License

MIT —— 自由使用、修改、分发。

---

**作者**：Danxin Liang · GitHub: [@liangdanxin8-max](https://github.com/liangdanxin8-max)
