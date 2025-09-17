# GitHub Actions 部署详细说明

## 步骤1: 创建GitHub仓库

1. 登录你的GitHub账户
2. 点击右上角的 "+" 号，选择 "New repository"
3. 仓库名称填写：`bing-auto-rewards`
4. 选择 "Public" 或 "Private"（建议Private保护账号安全）
5. 勾选 "Add a README file"
6. 点击 "Create repository"

## 步骤2: 上传代码

### 方法1: 使用Git命令行
```bash
# 克隆你的仓库
git clone https://github.com/你的用户名/bing-auto-rewards.git
cd bing-auto-rewards

# 复制项目文件到仓库目录
# 确保包含以下文件（账号配置将在Secrets中设置，无需提交accounts.json）：
# - .github/workflows/daily-checkin.yml
# - bingZDH.py
# - requirements.txt
# - README.md
# - .gitignore

# 提交代码
git add .
git commit -m "Initial commit: Bing auto rewards script"
git push origin main
```

### 方法2: 直接在GitHub网页上传
1. 在仓库页面点击 "Add file" → "Upload files"
2. 拖拽或选择项目文件
3. 填写提交信息，点击 "Commit changes"

## 步骤3: 设置GitHub Secrets

1. 进入你的仓库页面
2. 点击 "Settings" 标签
3. 左侧菜单选择 "Secrets and variables" → "Actions"
4. 点击 "New repository secret"
5. 名称填写：`ACCOUNTS_CONFIG`
6. 值填写你的账号配置JSON（注意格式要正确）。运行时脚本会直接从该Secret对应的环境变量中读取账号信息。

### 账号配置示例（存放在Secret中）：
```json
{
  "group1": [
    {
      "email": "your_email@example.com",
      "password": "your_password"
    }
  ],
  "group2": [
    {
      "email": "another_email@example.com",
      "password": "another_password"
    }
  ]
}
```

## 步骤4: 启用GitHub Actions

1. 进入你的仓库页面
2. 点击 "Actions" 标签
3. 如果看到 "Get started with GitHub Actions"，点击它
4. 选择 "Skip this: Set up a workflow yourself"
5. 系统会自动检测到 `.github/workflows/daily-checkin.yml` 文件

## 步骤5: 测试运行

1. 在 "Actions" 页面，你应该能看到 "Bing Daily Check-in" 工作流
2. 点击 "Run workflow" 按钮
3. 选择 "main" 分支，点击 "Run workflow"
4. 等待执行完成，查看结果

## 步骤6: 验证自动执行

1. 工作流配置为每天UTC时间2:00（北京时间10:00）自动执行
2. 你可以在 "Actions" 页面查看执行历史
3. 每次执行都会生成日志文件作为Artifact

## 故障排除

### 常见问题1: Chrome安装失败
- 确保工作流使用 `ubuntu-latest` 运行环境
- 检查Chrome安装命令是否正确

### 常见问题2: 依赖安装失败
- 检查 `requirements.txt` 文件格式
- 确保Python版本兼容（推荐3.9）

### 常见问题3: 账号配置错误
- 检查JSON格式是否正确（建议使用JSON校验工具）
- 确保账号密码没有特殊字符或已经正确转义
- 验证账号是否有效
- 确认仓库Secrets中的`ACCOUNTS_CONFIG`已设置且未过期

### 常见问题4: 执行超时
- GitHub Actions有6小时执行时间限制
- 如果账号较多，可能需要分批处理

## 安全建议

1. **使用Private仓库**：保护你的账号信息
2. **定期更换密码**：提高账号安全性
3. **监控执行日志**：及时发现异常情况
4. **备份重要数据**：定期备份账号配置

## 监控和维护

1. **查看执行状态**：每天检查Actions页面
2. **分析日志**：下载Artifact查看详细日志
3. **更新配置**：根据需要调整账号信息
4. **处理错误**：根据错误信息进行相应修复

## 高级配置

### 自定义执行时间
编辑 `.github/workflows/daily-checkin.yml` 文件中的cron表达式：
```yaml
schedule:
  - cron: '0 2 * * *'  # 每天UTC 2:00
  - cron: '0 14 * * *' # 每天UTC 14:00（北京时间22:00）
```

### 多环境部署
可以创建多个工作流文件，针对不同环境：
- `daily-checkin-prod.yml` - 生产环境
- `daily-checkin-test.yml` - 测试环境

### 通知配置
可以添加邮件或Slack通知，在任务完成或失败时发送通知。

## 技术支持

如果遇到问题：
1. 查看GitHub Actions执行日志
2. 检查工作流配置文件语法
3. 验证账号配置格式
4. 参考GitHub Actions官方文档

---

**注意**：本脚本仅供学习和个人使用，请遵守Bing Rewards的服务条款。
