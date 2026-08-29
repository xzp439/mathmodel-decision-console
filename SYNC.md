# 数学建模决策控制台 - 功能同步记录

**更新日期：** 2026-08-29
**网站地址：** https://xzp439.github.io/mathmodel-decision-console/
**GitHub仓库：** https://github.com/xzp439/mathmodel-decision-console
**本地路径：** C:\Users\34006\Doubao\chats\2026-08-28\new-chat-2\decision-map-app\

---

## 一、核心功能总览

### 1. 8个Gate工作流
| Gate | 名称 | 对应全局Skill | 主Agent角色 |
|---|---|---|---|
| G1 | 问题解析 | problem-parser + problem-classifier | 🔍 问题分析师 |
| G2 | 方法验证 | method-selector + related-paper-analyzer | 🧮 建模专家 |
| G2.5 | 方法选择 | method-selector + modeler-decision-logger | 🧮 建模专家 |
| G3 | 代码审查 | code-reviewer + python-code-reviewer + matlab-code-reviewer | 💻 程序员 |
| G4.5 | 结果判决 | result-report-generator + robustness-checker + final-method-explainer | 📊 结果分析师 |
| G4 | 结果冻结 | solution-package-builder | 📊 结果分析师 |
| G5 | 论文质量 | paper-section-writer + paper-polisher + figure-table-planner | ✍️ 论文写作专家 |
| G6 | 最终审计 | completeness-auditor + consistency-auditor + quality-assurance-auditor | 🛡️ 质量审计员 |

### 2. 多Agent协作系统
- **主Agent**：每个Gate由专门角色的Agent执行
- **评论家(⚖️)**：每个Gate执行后由评论家进行四维度审查
  - 逻辑严谨性
  - 数据准确性
  - 方法合理性
  - 表达清晰度
- **迭代机制**：评论家不通过则打回修改，最多2轮（共3轮输出）
- **对话记录**：可查看完整的Agent对话历史，包括每轮输出和评论家反馈

### 3. 全局Skill完整集成
- 22个全局skill的完整SKILL.md内容已嵌入网站（skills-full.js，455KB）
- 每个Gate执行时，对应skill的完整内容注入system prompt
- AI严格按照skill定义的工作流程、输入输出格式、质量检查标准执行

### 4. 多AI提供商支持（12个）
| 提供商 | 协议类型 | 特点 |
|---|---|---|
| 火山引擎/豆包 | OpenAI | 默认，国内 |
| OpenAI (GPT) | OpenAI | 国外 |
| Anthropic Claude | Anthropic | 自动适配协议 |
| Google Gemini | Gemini | 自动适配协议 |
| DeepSeek | OpenAI | 国内，代码强 |
| 通义千问 (Qwen) | OpenAI | 阿里 |
| 智谱AI (GLM) | OpenAI | 清华 |
| 月之暗面 (Kimi) | OpenAI | 长上下文 |
| Ollama (本地) | OpenAI | 免费，本地运行 |
| LM Studio (本地) | OpenAI | 本地GUI |
| OpenRouter (聚合) | OpenAI | 一个Key调所有 |
| 自定义 | OpenAI | 任何兼容接口 |

### 5. 多模型路由
- 每个Agent角色可独立配置模型
- 本地模型（含冒号如qwen2.5:7b）自动切换到Ollama本地API
- 云端模型使用当前默认提供商
- 执行时实时显示当前使用的模型名称

### 6. 模型预设（一键应用）
| 预设 | 配置 | 适用场景 |
|---|---|---|
| ☁️ 全云端 | 所有Agent用默认云端模型 | 追求质量 |
| ⚡ 混合模式(推荐) | G1/G6用本地qwen2.5:7b，其余云端 | 学生党，成本最优 |
| 🏠 全本地 | 所有Agent用本地Ollama不同模型 | 完全免费，隐私优先 |
| 🗑️ 清空 | 清除所有Agent专用配置 | 恢复默认 |

**混合模式详细配置：**
- 🔍 G1 问题分析师 → 本地 qwen2.5:7b（免费，读PDF token大）
- 🧮 G2/G2.5 建模专家 → 云端（强推理）
- 💻 G3 程序员 → 云端（代码理解）
- 📊 G4/G4.5 结果分析师 → 云端（敏感性分析）
- ✍️ G5 论文写作专家 → 云端（学术写作）
- 🛡️ G6 质量审计员 → 本地 qwen2.5:7b（免费，对照检查）
- ⚖️ 评论家 → 云端（质量把关最后防线）

### 7. 一键全流程执行
- 顶部栏「🚀 一键执行全部」按钮
- 按顺序自动执行8个Gate
- 实时进度显示（进度条、当前Gate、每个Gate状态）
- 每个Gate显示执行耗时
- 失败的Gate标记为红色，可后续单独重试
- 可随时取消执行
- 预计总耗时：3-5分钟（取决于API速度）

### 8. 文件管理系统
- 支持上传比赛题目、附录、数据等文件
- 分类管理（比赛题目、数据、附录、其他）
- PDF文本自动提取（用于G1问题解析）
- 文件保存在浏览器本地IndexedDB

### 9. 其他功能
- 判决系统：Accept / Edit / Reject 三态判决
- 状态持久化：所有配置和结果保存在localStorage
- 键盘快捷键：←→切换Gate，1/2/3判决
- 响应式设计：支持桌面和移动端
- 深色主题

---

## 二、当前配置状态

### 已完成
- ✅ 网站部署到GitHub Pages
- ✅ 12个AI提供商支持
- ✅ 22个全局skill完整内容嵌入
- ✅ 多Agent协作系统（主Agent+评论家）
- ✅ 多模型路由
- ✅ 4种模型预设
- ✅ 一键全流程执行
- ✅ 文件上传和PDF提取
- ✅ 火山引擎API Key已配置（用户自行保存，不在文档中记录）

### 待完成
- ⏳ Ollama软件安装（命令行下载太慢，需用户在浏览器下载）
- ⏳ qwen2.5:7b模型拉取（约4.7GB）
- ⏳ 本地模型测试验证
- ⏳ 混合模式实际运行测试

---

## 三、Ollama安装指南

### 步骤1：下载安装
1. 访问 https://ollama.com/
2. 点击「Download for Windows」
3. 运行 OllamaSetup.exe，一路下一步安装
4. 安装完成后Ollama会自动在后台运行

### 步骤2：拉取模型
打开命令行（PowerShell或CMD），执行：
```bash
ollama pull qwen2.5:7b
```
- 模型大小约4.7GB，需要几分钟到十几分钟
- 拉取完成后自动可用

### 步骤3：验证安装
```bash
ollama --version          # 查看版本
ollama list               # 查看已安装模型
ollama run qwen2.5:7b    # 运行模型测试
```

### 步骤4：网站配置
1. 打开 https://xzp439.github.io/mathmodel-decision-console/
2. 点击「⚙️ AI」
3. 选择默认云端提供商（火山引擎/DeepSeek等），填好API Key
4. 展开「🤖 按Agent角色配置不同模型」
5. 点击「⚡ 混合模式(推荐)」
6. 确认G1/G6显示为 qwen2.5:7b
7. 点击「保存设置」

---

## 四、版本更新记录

| 版本 | 功能 |
|---|---|
| v1-v9 | 基础决策地图、8个Gate、判决系统、文件管理 |
| v10 | 全局skill集成（简化版prompt模板） |
| v11 | 一键全流程自动执行 |
| v12 | 全局skill完整内容集成（22个skill，455KB） |
| v13 | 多Agent协作系统（主Agent+评论家，最多2轮迭代） |
| v14 | 多模型路由（每个Agent可配置不同模型） |
| v15 | 多AI提供商支持（12个提供商，3种协议自动适配） |
| v16 | 模型预设（全云端/混合模式/全本地/清空，一键应用） |

---

## 五、使用流程

### 快速开始
1. 打开网站：https://xzp439.github.io/mathmodel-decision-console/
2. 配置AI：「⚙️ AI」→ 选择提供商 → 填API Key → 保存
3. 上传题目：文件库 → 比赛题目 → 上传PDF
4. 执行：点击「🚀 一键执行全部」
5. 审核：逐个Gate查看AI结果，Accept/Edit/Reject
6. 导出：完成后复制各Gate结果用于论文写作

### 混合模式（推荐）
1. 先安装Ollama并拉取qwen2.5:7b
2. 配置云端API Key
3. AI设置 → 应用「⚡ 混合模式」预设
4. 保存并执行

---

## 六、技术栈

- **前端**：纯HTML/CSS/JavaScript，单文件应用
- **AI API**：OpenAI兼容格式（chat/completions），支持Anthropic和Gemini协议转换
- **本地存储**：localStorage（配置）+ IndexedDB（文件）
- **PDF解析**：PDF.js (v3.11.174)
- **部署**：GitHub Pages
- **模型预设文件**：skills-full.js（22个全局skill完整内容）

---

*本文档随网站功能更新持续同步*
