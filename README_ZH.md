

---

## 目录

- [🤔 什么是规格驱动开发?](#-什么是规格驱动开发)
- [⚡ 快速开始](#-快速开始)
- [🤖 支持的 AI 智能体](#-支持的-ai-智能体)
- [💬 支持](#-支持)
- [🙏 致谢](#-致谢)
- [📄 许可证](#-许可证)

## 🤔 什么是规格驱动开发？

规格驱动开发（Spec-Driven Development，简称 SDD）**颠覆了传统软件开发的方式**。几十年来，代码一直是王道——规格说明只是我们搭建的脚手架，一旦"真正的编码工作"开始，就会被丢弃。规格驱动开发改变了这一点：**规格说明变得可执行**，它们直接生成可工作的实现，而不仅仅是指导实现。

## ⚡ 快速开始

### 1. 安装 Specify CLI

**推荐：持久化安装**

一次安装，随处使用：

```bash
# 安装
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git

# 使用
specify init <PROJECT_NAME>
specify check

# 升级
uv tool install specify-cli --force --from git+https://github.com/github/spec-kit.git
```

**可选：一次性使用**

无需安装直接运行：

```bash
uvx --from git+https://github.com/github/spec-kit.git specify init <PROJECT_NAME>
```

持久化安装的优势：工具保持安装状态并在 PATH 中可用、无需创建 shell 别名、可以使用 `uv tool list`/`upgrade`/`uninstall` 管理工具、更简洁的 shell 配置。

### 2.使用场景示例

#### 基本使用

```bash
# 创建新项目
specify init my-project

# 指定 AI 助手
specify init my-project --ai claude

# 检查系统要求
specify check
```

#### 在当前目录初始化

```bash
# 方式 1：使用 .
specify init . --ai copilot

# 方式 2：使用 --here
specify init --here --ai copilot

# 强制覆盖（跳过确认）
specify init . --force --ai claude
specify init . --force --ai qwen
```

#### 高级选项

```bash
# PowerShell 脚本（Windows）
specify init my-project --ai copilot --script ps

# 调试模式
specify init my-project --ai claude --debug

# 使用 GitHub 令牌（企业环境）
specify init my-project --ai claude --github-token ghp_your_token_here

# 跳过工具检查
specify init my-project --ai claude --ignore-agent-tools
```



### 3. 规格驱动开发工作流

在项目目录中启动你的 AI 助手，按以下步骤进行开发：

#### 步骤 1：建立项目原则

```bash
/speckit.constitution 
​```
一、强制约束
  1. 禁止未授权Git操作 - 所有git add/commit/push/merge等操作必须获得用户明确授权
  2. 禁止使用Windows语法 - Git Bash环境下使用/dev/null而非nul，避免创建无法删除的文件
  3. 始终使用中文与我沟通交流，并且所产出的文档也使用中文，然后代码注释也使用中文
二、开发原则
  1. 无历史包袱原则 - 无需向后兼容、无需迁移脚本、无需保留旧代码
  2. 最少文件原则 - 避免创建不必要的文件、抽象层、工具类
  3. 最全功能原则 - 实现完整功能，不偷工减料
  4. 最简代码原则 - 使用最直接的实现方式，积极重构删除冗余
  5. 以函数/方法为最小测试单元，及时执行单元测试；每完成一个MVP单元，立即运行集成测试
三、文档规范
  1. 变更必须记录 - 所有定制化功能必须在custom-features/变更日志.md中记录
  2. 优先查阅变更日志 - 实现功能前先查看对应模块的变更日志
  3. 代码与文档同步 - 代码变更和文档更新必须在同一次提交
​```
```

#### 步骤 2：创建规格说明

```bash
/speckit.specify 构建一个应用程序，帮助我将照片组织到不同的相册中。相册按日期分组，可以在主页面上通过拖放重新组织。相册不会嵌套在其他相册中。在每个相册内，照片以瓦片式界面预览。
```

#### 步骤 3：澄清规格说明（直接执行）

```bash
/speckit.clarify  # 澄清规格不足的区域，减少下游返工
```

#### 步骤 3.1：质量检查清单（直接执行且可选）

```bash
/speckit.checklist  # 生成质量检查清单，验证需求的完整性、清晰度和一致性
```

#### 步骤 4：创建技术实施计划

```bash
/speckit.plan 应用程序使用 Vite，库的数量最少。尽可能使用原生 HTML、CSS 和 JavaScript。图片不会上传到任何地方，元数据存储在本地 SQLite 数据库中。
```

#### 步骤 5：分解为任务（直接执行）

```bash
/speckit.tasks
```

#### 步骤 5.1：一致性分析（直接执行且可选）

```bash
/speckit.analyze  # 跨工件一致性和覆盖率分析，建议在执行实施之前运行
```

#### 步骤 6：执行实施（直接执行）

```bash
/speckit.implement
```

## 🤖 支持的 AI 智能体

| 智能体                                                     | 支持状态 | 备注                                             |
|-----------------------------------------------------------|---------|---------------------------------------------------|
| [Claude Code](https://www.anthropic.com/claude-code)      | ✅ |                                                   |
| [GitHub Copilot](https://code.visualstudio.com/)          | ✅ |                                                   |
| [Gemini CLI](https://github.com/google-gemini/gemini-cli) | ✅ |                                                   |
| [Cursor](https://cursor.sh/)                              | ✅ |                                                   |
| [Qwen Code](https://github.com/QwenLM/qwen-code)          | ✅ |                                                   |
| [opencode](https://opencode.ai/)                          | ✅ |                                                   |
| [Windsurf](https://windsurf.com/)                         | ✅ |                                                   |
| [Kilo Code](https://github.com/Kilo-Org/kilocode)         | ✅ |                                                   |
| [Auggie CLI](https://docs.augmentcode.com/cli/overview)   | ✅ |                                                   |
| [CodeBuddy CLI](https://www.codebuddy.ai/cli)             | ✅ |                                                   |
| [Roo Code](https://roocode.com/)                          | ✅ |                                                   |
| [Codex CLI](https://github.com/openai/codex)              | ✅ |                                                   |
| [Amp](https://ampcode.com/) | ✅ | |
| [Amazon Q Developer CLI](https://aws.amazon.com/developer/learning/q-developer-cli/) | ⚠️ | [不支持](https://github.com/aws/amazon-q-developer-cli/issues/3064)斜杠命令的自定义参数 |



规格驱动开发是一个结构化的流程，强调：

- **意图驱动开发**，其中规格说明在"怎么做"之前定义"做什么"
- **使用护栏和组织原则创建丰富的规格说明**
- **多步骤细化**，而不是从提示一次性生成代码
- **严重依赖**高级 AI 模型的能力进行规格说明解释

## 🙏 致谢

该项目深受 [John Lam](https://github.com/jflam) 的工作和研究的影响和启发。

## 📄 许可证

该项目根据 MIT 开源许可证的条款获得许可。有关完整条款，请参阅 [LICENSE](./LICENSE) 文件。
