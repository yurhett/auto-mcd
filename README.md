# auto-mcd

自动领取麦当劳优惠券的 GitHub Actions 工作流项目。

![](https://open.mcd.cn/static/media/hero-bg.349a0979.jpg)


## 项目功能

- 每天自动运行脚本领取麦当劳优惠券
- 支持手动触发执行
- 执行结果会保存到 GitHub Actions 作业摘要中，方便查看

## 使用方法

### 1. Fork 项目

点击 GitHub 页面右上角的 "Fork" 按钮，将此项目复刻到您的 GitHub 账户中。

### 2. 获取 MCP_TOKEN

MCP_TOKEN 需要从麦当劳开放平台获取：

1. 访问 [麦当劳开放平台](https://open.mcd.cn/mcp)
2. 注册或登录您的麦当劳开放平台账号
3. 在页面中找到并复制您的 MCP 令牌（Token）

### 3. 配置 MCP_TOKEN 机密

1. 进入您复刻后的项目页面
2. 点击 "Settings"（设置）
3. 在左侧菜单中选择 "Secrets and variables" → "Actions"
4. 点击 "New repository secret"（新建仓库机密）
5. 名称填写为 `MCP_TOKEN`
6. 在 "Secret" 字段中粘贴您从麦当劳开放平台获取的 MCP 令牌
7. 点击 "Add secret"（添加机密）

### 3. 启用工作流

1. 进入项目的 "Actions"（操作）页面
2. 点击 "Run Script" 工作流
3. 点击 "Enable workflow"（启用工作流）

## 工作流说明

### 自动执行

工作流会每天在北京时间0点（UTC时间16点）自动执行，无需手动干预。

### 手动触发

1. 进入项目的 "Actions" 页面
2. 点击 "Run Script" 工作流
3. 点击 "Run workflow" 按钮
4. 在弹出的对话框中，您可以选择输入 `mcp_token` 参数（可选，不输入则会使用仓库机密中配置的值）
5. 点击 "Run workflow" 执行

## 调试指南

### 查看执行结果

每次工作流执行完成后，您可以在 "Actions" 页面查看执行结果：

1. 进入 "Actions" 页面
2. 点击具体的执行记录
3. 查看 "Run Script" 作业
4. 滚动到页面底部可以看到 "Job summary"（作业摘要），其中包含了脚本执行的完整输出

### 使用 workflow_dispatch 调试

1. 点击 "Run workflow" 手动触发执行
2. 在输入框中填写测试用的 MCP 令牌（可选）
3. 观察执行过程和输出结果
4. 根据输出结果调试代码（如果需要）

## 技术细节

- 使用 Bun 作为 JavaScript 运行时
- 工作流配置文件位于 `.github/workflows/run-script.yml`
- 主入口文件为 `index.ts`

## 本地开发

如果您需要在本地开发和测试：

```bash
# 安装依赖
bun install

# 运行脚本
bun start
```

注意：在本地运行时，需要设置环境变量 `MCP_TOKEN`。
