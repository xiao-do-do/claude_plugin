# Claude Code 插件市场

Claude Code 插件市场 - 收集和分享高质量的 Claude Code 插件。

## 什么是 Claude Code 插件？

Claude Code 插件可以扩展 Claude Code 的功能，提供自定义命令、专业代理、技能等。插件可以帮助你：

- 添加自定义工作流程和命令
- 提供专业领域的代理（如测试、审查、研究等）
- 集成外部工具和服务
- 自定义 Claude Code 的行为

## 安装插件

### 方式1：从插件市场安装（推荐）

```bash
# 1. 添加插件市场
/plugin marketplace add xiao-do-do/claude_plugin

# 2. 安装插件
/plugin install riper-5@claude-plugin-market
```

### 方式2：本地测试安装

```bash
# 克隆仓库
git clone https://github.com/xiao-do-do/claude_plugin.git

# 添加本地市场
/plugin marketplace add ./claude_plugin

# 安装插件
/plugin install riper-5@claude-plugin-market
```

## 可用插件

### RIPER-5 严格模式协议

**描述**: RIPER-5 严格模式协议 - 研究/创新/计划/执行/审查

**功能**:
- 🔍 **研究模式**: 深度代码分析，理解代码结构和架构
- 💡 **创新模式**: 头脑风暴多种解决方案
- 📋 **计划模式**: 创建详尽的技术规范
- ⚡ **执行模式**: 严格按照计划实施
- ✅ **审查模式**: 验证实施与计划的符合程度
- 🧪 **测试模式**: 设计和执行全面的测试

**安装**:
```bash
claude-code plugin install https://github.com/xiao-do-do/claude_plugin/plugins/riper-5
```

**使用**:
```bash
# 启动 RIPER-5 协议
/riper-5

# 或者带任务描述
/riper-5 实现用户认证功能
```

## 插件管理

```bash
# 列出已安装的插件
claude-code plugin list

# 启用插件
claude-code plugin enable <plugin-name>

# 禁用插件
claude-code plugin disable <plugin-name>

# 卸载插件
claude-code plugin uninstall <plugin-name>

# 更新插件
claude-code plugin update <plugin-name>
```

## 创建自己的插件

查看 [插件开发指南](./docs/plugin-development.md) 了解如何创建自己的插件。

### 基本插件结构

```
my-plugin/
├── .claude-plugin/
│   └── plugin.json          # 插件元数据
├── commands/                # 自定义命令（可选）
│   └── my-command.md
├── agents/                  # 专业代理（可选）
│   └── my-agent.md
└── skills/                  # 技能（可选）
    └── my-skill/
        └── SKILL.md
```

### plugin.json 示例

```json
{
  "name": "my-plugin",
  "description": "我的 Claude Code 插件",
  "version": "1.0.0",
  "author": {
    "name": "Your Name"
  }
}
```

## 贡献插件

欢迎贡献你的插件到这个市场！

1. Fork 这个仓库
2. 在 `plugins/` 目录下创建你的插件目录
3. 确保插件包含完整的 `.claude-plugin/plugin.json` 文件
4. 更新 README.md 添加你的插件信息
5. 提交 Pull Request

## 插件质量标准

提交到市场的插件应该：

- ✅ 包含完整的 `plugin.json` 配置
- ✅ 提供清晰的描述和使用说明
- ✅ 遵循 Claude Code 插件规范
- ✅ 代码质量良好，无明显错误
- ✅ 尊重用户隐私和安全

## 资源

- [Claude Code 官方文档](https://code.claude.com/docs)
- [插件参考文档](https://code.claude.com/docs/en/plugins-reference)
- [插件开发指南](https://code.claude.com/docs/en/plugins)

## 许可证

本仓库采用 MIT 许可证。各个插件可能有自己的许可证，请查看插件目录中的 LICENSE 文件。

## 问题反馈

如果你在使用插件时遇到问题，请在 [Issues](https://github.com/xiao-do-do/claude_plugin/issues) 中反馈。
