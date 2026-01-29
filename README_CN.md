[English](README.md) | [中文](README_CN.md)

# 🎯 价值投资助手 (Value Investing Agent)

一个 AI 驱动的价值投资分析助手。基于本杰明·格雷厄姆和沃伦·巴菲特的投资哲学分析股票。

> *"价格是你付出的，价值是你得到的。"* - 沃伦·巴菲特

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Node.js Version](https://img.shields.io/badge/node-%3E%3D18.0.0-brightgreen)](https://nodejs.org/)
[![MCP](https://img.shields.io/badge/MCP-Compatible-blue)](https://modelcontextprotocol.io/)

## ⚠️ 免责声明

**本工具仅供学习和研究目的，不构成任何投资建议。投资有风险，入市需谨慎。作者不对基于本工具做出的任何投资决策承担责任。**

## ✨ 功能特点

- 📊 **实时股票数据** - 报价、财务报表、公司简介
- 🧮 **内在价值计算** - DCF 模型和格雷厄姆数字
- 🏰 **护城河分析** - 评估公司竞争优势
- 📰 **新闻聚合** - 追踪自选股相关新闻
- 📝 **报告生成** - 每日汇总和深度分析报告
- 🔌 **可插拔数据源** - 轻松添加自定义数据源

## 🚀 快速开始

### 环境要求

- Node.js >= 18.0.0
- 任意支持 MCP 协议的客户端（Claude Desktop、Claude Code 或你自己的应用）

> **说明：** 这是一个独立的 MCP 服务器，可以在 Windows、macOS 或 Linux 上运行。它可以与任何支持 [Model Context Protocol](https://modelcontextprotocol.io/) 的应用配合使用，不仅限于 Claude 产品。

### 安装方式

#### 方式一：npx 直接运行（推荐）

无需安装，直接配置 MCP：

```json
{
  "mcpServers": {
    "value-investing-agent": {
      "command": "npx",
      "args": ["-y", "value-investing-agent"]
    }
  }
}
```

#### 方式二：全局安装

```bash
npm install -g value-investing-agent
```

MCP 配置：

```json
{
  "mcpServers": {
    "value-investing-agent": {
      "command": "value-investing-agent"
    }
  }
}
```

#### 方式三：从源码安装

```bash
git clone https://github.com/danielchu97/Value-Investing-Agent.git
cd value-investing-agent
npm install
npm run build
```

MCP 配置：

```json
{
  "mcpServers": {
    "value-investing-agent": {
      "command": "node",
      "args": ["/path/to/value-investing-agent/dist/index.js"]
    }
  }
}
```

### 配置文件位置

**Claude Desktop:**
- macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
- Windows: `%APPDATA%\Claude\claude_desktop_config.json`

## 📖 使用示例

### 获取股票报价

```
"获取苹果公司的当前报价"
"MSFT 现在的价格是多少？"
```

### 分析内在价值

```
"计算 AAPL 的内在价值"
"用 DCF 模型分析亚马逊的合理估值"
```

### 评估经济护城河

```
"分析可口可乐的竞争护城河"
"微软有宽护城河吗？"
```

### 管理自选股

```
"把 GOOGL 添加到我的自选股，放在科技组"
"显示我的自选股列表"
"从自选股中删除 TSLA"
```

### 生成报告

```
"为我的自选股生成每日报告"
"生成伯克希尔哈撒韦的详细分析报告"
```

## 🔧 可用工具

| 工具 | 描述 |
|------|------|
| `get_stock_quote` | 获取实时股票报价和指标 |
| `get_financials` | 获取财务报表（利润表、资产负债表、现金流量表）|
| `calculate_intrinsic_value` | DCF 和格雷厄姆估值，含安全边际分析 |
| `analyze_moat` | 评估公司竞争优势 |
| `get_news` | 获取股票相关新闻 |
| `manage_watchlist` | 管理个人自选股列表 |
| `generate_daily_report` | 生成自选股每日汇总 |
| `generate_stock_report` | 生成完整的价值投资分析报告 |
| `set_provider` | 切换数据源 |
| `list_providers` | 列出可用数据源 |

## 🔌 数据源配置

插件化架构允许您添加自己的数据源。详见 [自定义数据源指南](docs/custom-provider.md)。

### 内置数据源

| 数据源 | API 密钥 | 速率限制 | 适用场景 |
|--------|----------|----------|----------|
| **yahoo-finance**（默认）| 不需要 | 有限制（可能遇到 429 错误）| 快速测试 |
| **finnhub** | 需要（免费）| 60 次/分钟 | 生产环境（推荐）|
| **alpha-vantage** | 需要（免费）| 5 次/分钟 | 基本数据需求 |

### 配置 API 密钥

**Finnhub**（推荐，稳定可靠）：
1. 在 [finnhub.io/register](https://finnhub.io/register) 注册获取免费 API 密钥
2. 设置环境变量：
   ```bash
   export FINNHUB_API_KEY=你的API密钥
   ```
   或在 Claude Desktop 配置中设置：
   ```json
   {
     "mcpServers": {
       "value-investing-agent": {
         "command": "npx",
         "args": ["-y", "value-investing-agent"],
         "env": {
           "FINNHUB_API_KEY": "你的API密钥"
         }
       }
     }
   }
   ```

**Alpha Vantage**：
1. 在 [alphavantage.co](https://www.alphavantage.co/support/#api-key) 获取免费 API 密钥
2. 设置环境变量：`ALPHA_VANTAGE_API_KEY=你的密钥`

### 切换数据源

```
"切换到 finnhub 数据源"
"使用 alpha-vantage 获取数据"
"列出可用的数据源"
```

### 添加自定义数据源

1. 复制 `src/providers/provider-template.ts`
2. 实现 `DataProvider` 接口
3. 在 `src/providers/index.ts` 中注册

```typescript
import { MyProvider } from './my-provider';
registerProvider('my-provider', (config) => new MyProvider(config));
```

## 🎓 价值投资原则

本工具基于经典的价值投资理念：

### 1. 内在价值 (Intrinsic Value)
公司的真实价值由其未来现金流的现值决定，而非市场价格。

### 2. 安全边际 (Margin of Safety)
只在价格显著低于内在价值时买入（至少 25% 折扣）。

### 3. 经济护城河 (Economic Moat)
寻找具有持久竞争优势的公司，保护其长期利润。

### 4. 能力圈 (Circle of Competence)
只投资于你能理解的业务。

### 5. 市场先生 (Mr. Market)
把市场情绪波动当作机会，而不是被其左右。

## 📊 关键指标

### 估值指标
- 市盈率（P/E）: < 15（低估）
- 市净率（P/B）: < 1.5（低估）
- 格雷厄姆数字：防御型投资者的价格上限

### 盈利能力
- 净资产收益率（ROE）: > 15%（优秀）
- 毛利率: > 40%（定价权）
- 净利率: > 10%（高效）

### 财务安全
- 流动比率: > 1.5（流动性充足）
- 负债权益比: < 1.0（保守）
- 利息覆盖率: > 5 倍（安全）

## 🛠️ 开发指南

```bash
# 安装依赖
npm install

# 构建
npm run build

# 开发模式（监听文件变化）
npm run dev

# 运行测试
npm test

# 代码检查
npm run lint
```

## 📁 项目结构

```
value-investing-agent/
├── src/
│   ├── index.ts              # 入口文件
│   ├── server.ts             # MCP 服务器
│   ├── providers/            # 数据源
│   ├── tools/                # MCP 工具
│   ├── analysis/             # 分析引擎
│   ├── utils/                # 工具函数
│   ├── config/               # 配置管理
│   └── types/                # TypeScript 类型
├── skills/                   # Claude 技能
├── data/                     # 本地数据（自选股、缓存）
├── docs/                     # 文档
└── tests/                    # 测试文件
```

## 🤝 参与贡献

欢迎贡献代码！请在提交 PR 前阅读贡献指南。

1. Fork 本仓库
2. 创建功能分支
3. 进行修改
4. 运行测试
5. 提交 Pull Request

## 📜 开源协议

MIT License - 详见 [LICENSE](LICENSE)

## 🙏 致谢

本项目受以下投资大师的智慧启发：

- **本杰明·格雷厄姆** - 《聪明的投资者》、《证券分析》
- **沃伦·巴菲特** - 伯克希尔·哈撒韦股东信
- **查理·芒格** - 《穷查理宝典》

## 📚 推荐阅读

- [《聪明的投资者》](https://book.douban.com/subject/5243775/) - 本杰明·格雷厄姆
- [巴菲特致股东的信](https://www.berkshirehathaway.com/letters/letters.html)
- [价值投资指南](docs/value-investing-guide.md)

---

**记住：** *"股市的设计就是把钱从急躁的人手中转移到有耐心的人手中。"* - 沃伦·巴菲特
