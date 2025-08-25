# Bing 自动签到脚本

这是一个自动化的Bing Rewards签到脚本，支持多账号并行处理，可以自动完成登录、签到、点击任务和搜索赚积分等操作。

## 功能特性

- 🔐 自动登录多个Bing账号
- ✅ 自动签到获取积分
- 🎯 自动点击积分任务卡片
- 🔍 自动搜索赚取积分
- 🌐 支持无头模式运行
- 📱 多账号组并行处理
- 🚀 支持GitHub Actions自动执行

## 部署方式

### 方式1: GitHub Actions（推荐）

1. **Fork本仓库**到你的GitHub账户

2. **设置GitHub Secrets**：
   - 进入你的仓库 → Settings → Secrets and variables → Actions
   - 添加新的secret，名称为`ACCOUNTS_CONFIG`
   - 值为你的账号配置JSON内容（见下方格式）

3. **账号配置格式**：
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

4. **自动执行**：
   - 脚本会在每天UTC时间2:00（北京时间10:00）自动执行
   - 也可以手动触发：Actions → Bing Daily Check-in → Run workflow

### 方式2: 本地运行

1. **安装依赖**：
   ```bash
   pip install -r requirements.txt
   ```

2. **配置账号**：
   - 编辑`accounts.json`文件，添加你的账号信息

3. **运行脚本**：
   ```bash
   # 执行一次
   python bingZDH.py
   
   # 或指定参数
   python bingZDH.py --once    # 执行一次
   python bingZDH.py --auto    # 每天凌晨2点自动执行
   ```

## 注意事项

⚠️ **重要提醒**：
- 请确保你的账号信息安全，不要在公开代码中暴露密码
- 建议使用GitHub Secrets存储敏感信息
- 脚本使用无头模式运行，适合服务器环境
- 支持多账号组并行处理，提高执行效率

## 日志和监控

- 执行日志会保存在`bing_automation.log`文件中
- 在GitHub Actions中，日志会作为Artifact上传，保留7天
- 如果出现错误，会生成截图文件用于调试

## 故障排除

### 常见问题

1. **Chrome启动失败**：
   - 确保系统已安装Chrome浏览器
   - 检查网络连接是否正常

2. **登录失败**：
   - 检查账号密码是否正确
   - 确认账号没有被锁定或需要验证

3. **搜索任务失败**：
   - 检查网络连接
   - 确认Bing服务是否正常

### 获取帮助

如果遇到问题，请检查：
1. 执行日志中的错误信息
2. 生成的截图文件
3. GitHub Actions的执行记录

## 许可证

本项目仅供学习和个人使用，请遵守相关服务条款。

## 贡献

欢迎提交Issue和Pull Request来改进这个项目！
