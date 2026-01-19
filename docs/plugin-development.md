# Claude Code 插件开发指南

本指南将帮助你创建自己的 Claude Code 插件。

## 插件结构

一个标准的 Claude Code 插件包含以下结构：

```
my-plugin/
├── .claude-plugin/
│   └── plugin.json          # 插件元数据（必需）
├── commands/                # 自定义命令（可选）
│   └── my-command.md
├── agents/                  # 专业代理（可选）
│   └── my-agent.md
├── skills/                  # 技能（可选）
│   └── my-skill/
│       └── SKILL.md
├── hooks/                   # 钩子（可选）
│   └── my-hook.sh
└── README.md               # 插件说明（推荐）
```

## plugin.json 配置

`plugin.json` 是插件的核心配置文件，必须放在 `.claude-plugin/` 目录下。

### 基本配置

```json
{
  "name": "my-plugin",
  "description": "我的 Claude Code 插件",
  "version": "1.0.0",
  "author": {
    "name": "Your Name",
    "email": "your.email@example.com",
    "url": "https://github.com/yourusername"
  }
}
```

### 完整配置示例

```json
{
  "name": "my-plugin",
  "description": "我的 Claude Code 插件",
  "version": "1.0.0",
  "author": {
    "name": "Your Name",
    "email": "your.email@example.com",
    "url": "https://github.com/yourusername"
  },
  "license": "MIT",
  "homepage": "https://github.com/yourusername/my-plugin",
  "repository": {
    "type": "git",
    "url": "https://github.com/yourusername/my-plugin.git"
  },
  "keywords": ["claude", "plugin", "automation"]
}
```

## 创建命令（Commands）

命令是用户可以通过 `/command-name` 调用的自定义功能。

### 命令文件格式

在 `commands/` 目录下创建 Markdown 文件，使用 frontmatter 定义命令元数据：

```markdown
---
description: 命令的简短描述
argument-hint: 可选参数提示
---

# 命令名称

命令的详细说明和使用指南。

## 功能

- 功能1
- 功能2

## 使用示例

\`\`\`bash
/my-command 参数
\`\`\`

## 注意事项

使用命令时的注意事项。
```

### 示例：代码审查命令

```markdown
---
description: 执行代码审查并提供改进建议
argument-hint: 可选文件路径
---

# 代码审查命令

自动审查代码质量、安全性和最佳实践。

## 功能

- 检查代码质量问题
- 识别安全漏洞
- 提供改进建议
- 验证代码规范

## 使用方法

\`\`\`bash
# 审查当前目录
/code-review

# 审查特定文件
/code-review src/main.py
\`\`\`
```

## 创建代理（Agents）

代理是专门处理特定任务的 AI 助手，Claude 会根据任务上下文自动调用。

### 代理文件格式

在 `agents/` 目录下创建 Markdown 文件：

```markdown
---
name: agent-name
description: 代理的简短描述
tools: Glob, Grep, Read, Bash
model: sonnet
color: blue
---

# 代理名称

代理的详细说明，包括专长领域和使用场景。

## 核心使命

描述代理的主要职责。

## 能力

- 能力1
- 能力2
- 能力3

## 使用场景

描述何时应该使用这个代理。
```

### Frontmatter 字段说明

- `name`: 代理的唯一标识符
- `description`: 简短描述（显示在代理列表中）
- `tools`: 代理可以使用的工具列表（用逗号分隔）
- `model`: 使用的模型（sonnet, opus, haiku）
- `color`: 代理的显示颜色

### 可用工具列表

- `Glob` - 文件模式匹配
- `Grep` - 内容搜索
- `Read` - 读取文件
- `Write` - 写入文件
- `Edit` - 编辑文件
- `Bash` - 执行命令
- `Task` - 启动子任务
- `TodoWrite` - 任务管理
- `WebFetch` - 获取网页内容
- `WebSearch` - 网页搜索

### 示例：测试代理

```markdown
---
name: test-agent
description: 专业测试代理，设计和执行全面的测试用例
tools: Glob, Grep, Read, Bash, TodoWrite
model: sonnet
color: green
---

# 测试代理

专业的软件测试专家，专注于设计和执行全面的测试方案。

## 核心使命

运用专业的软件测试知识，设计全面的测试用例，尽可能发现潜在的 BUG。

## 测试方法

- 等价类划分
- 边界值分析
- 决策表测试
- 状态转换测试

## 测试类型

- 单元测试
- 集成测试
- API 测试
- 端到端测试
```

## 创建技能（Skills）

技能是 Claude 可以自主调用的功能模块。

### 技能目录结构

```
skills/
└── my-skill/
    ├── SKILL.md
    └── resources/
        └── templates/
```

### SKILL.md 格式

```markdown
---
description: 技能的简短描述
argument-hint: 可选参数提示
---

# 技能名称

技能的详细说明。

## 功能

技能提供的功能列表。

## 使用场景

描述何时应该使用这个技能。
```

## 测试插件

### 本地测试

```bash
# 安装插件到本地
claude-code plugin install /path/to/your/plugin

# 启用插件
claude-code plugin enable your-plugin-name

# 测试命令
/your-command

# 查看插件状态
claude-code plugin list
```

### 调试

```bash
# 查看插件详细信息
claude-code plugin info your-plugin-name

# 重新加载插件
claude-code plugin update your-plugin-name
```

## 发布插件

### 1. 准备发布

- 确保 `plugin.json` 包含完整信息
- 编写清晰的 README.md
- 添加使用示例和文档
- 测试所有功能

### 2. 版本管理

使用语义化版本号（Semantic Versioning）：

- `1.0.0` - 主版本.次版本.修订号
- 主版本：不兼容的 API 变更
- 次版本：向后兼容的功能新增
- 修订号：向后兼容的问题修正

### 3. 发布到 Git

```bash
# 初始化 Git 仓库
git init
git add .
git commit -m "Initial commit"

# 推送到 GitHub
git remote add origin https://github.com/yourusername/your-plugin.git
git push -u origin main

# 创建版本标签
git tag v1.0.0
git push origin v1.0.0
```

### 4. 提交到插件市场

1. Fork [claude_plugin](https://github.com/xiao-do-do/claude_plugin) 仓库
2. 在 `plugins/` 目录下添加你的插件
3. 更新 README.md 添加插件信息
4. 提交 Pull Request

## 最佳实践

### 命名规范

- 插件名称：使用小写字母和连字符（如 `my-plugin`）
- 命令名称：简短且描述性（如 `code-review`）
- 代理名称：使用连字符分隔（如 `test-agent`）

### 文档规范

- 提供清晰的使用说明
- 包含实际使用示例
- 说明依赖和要求
- 添加故障排除指南

### 代码质量

- 遵循 Markdown 格式规范
- 使用清晰的描述和说明
- 测试所有功能
- 处理边界情况

### 安全考虑

- 不要在插件中硬编码敏感信息
- 验证用户输入
- 使用环境变量存储配置
- 遵循最小权限原则

## 示例插件

查看 [riper-5](../plugins/riper-5) 插件作为完整示例。

## 资源

- [Claude Code 官方文档](https://code.claude.com/docs)
- [插件参考文档](https://code.claude.com/docs/en/plugins-reference)
- [插件市场](https://github.com/xiao-do-do/claude_plugin)

## 获取帮助

如果你在开发插件时遇到问题：

1. 查看 [官方文档](https://code.claude.com/docs/en/plugins-reference)
2. 参考现有插件示例
3. 在 [Issues](https://github.com/xiao-do-do/claude_plugin/issues) 中提问
