# CFMemos

一个基于 Cloudflare 平台构建的 Memos 应用，提供轻量级的笔记和备忘录功能。

## 🌟 项目特性

- **后端架构**: Cloudflare Workers + D1 + R2
- **前端部署**: Cloudflare Pages
- **版本兼容**: 基于 Memos 经典版本 0.18.1
- **API 兼容**: 遵循 0.18.1 API 规范并稍作调整

## 📋 功能说明

### 保留功能
- 完整的 Memos 核心功能
- 笔记创建、编辑、删除
- 标签管理
- 搜索功能

### 移除/调整功能
- **S3 存储**: 使用 Cloudflare R2 替代
- **上传限制**: 硬编码为 32MB
- **自动备份**: 移除此功能设置

## 🚀 快速开始

### 环境要求

- Node.js 20 或更高版本
- Wrangler CLI
- Cloudflare 账号
- Git

### 后端部署

#### 1. 克隆项目
```bash
git clone https://github.com/jkjoy/cfmemos.git
cd cfmemos/backend
```

#### 2. 安装依赖
```bash
npm install
```

#### 3. 登录 Cloudflare
```bash
wrangler login
```

#### 4. 创建数据库
```bash
wrangler d1 create memos_db
```

记录下生成的 database id，并更新 `wrangler.toml` 文件中的 `database_id` 配置。

#### 5. 初始化数据库
```bash
# 方式一：使用 npm 脚本
npm run db:init

# 方式二：直接执行 SQL 文件
wrangler d1 execute memos_db --file=./schema.sql
```

#### 6. 创建存储桶
```bash
wrangler r2 bucket create memos
```

#### 7. 部署后端
```bash
wrangler deploy
```

> 💡 提示：如果只需要 API 功能，部署到此步骤即可完成。API 文档可参考官方 Memos API 文档，基本保持一致。

### 前端部署

#### 1. 进入前端目录
```bash
cd ../frontend
```

#### 2. 安装依赖
```bash
npm install
```

#### 3. 构建项目
```bash
npm run build
```

#### 4. 部署到 Cloudflare Pages
```bash
wrangler pages deploy dist --project-name=memos-frontend
```

#### 5. 配置环境变量
部署成功后，在 Cloudflare Pages 项目中：
1. 找到 `memos-frontend` 项目
2. 进入「设置」→「绑定」
3. 确认环境变量配置：
   - **变量名**: `BACKEND`
   - **值**: `memos-api`

## 📖 API 文档

API 接口遵循 Memos 0.18.1 版本规范，具体接口文档可参考：
- [Memos 官方 API 文档](https://usememos.com/docs/api)

## 🔧 配置说明

### 数据库配置
- 使用 Cloudflare D1 作为数据库
- 自动初始化表结构

### 文件存储
- 使用 Cloudflare R2 作为文件存储
- 支持最大 32MB 文件上传

## 🤝 贡献

欢迎提交 Issue 和 Pull Request 来改进这个项目！

## 📄 许可证

本项目基于 MIT 许可证开源。

## 🔗 相关链接

- [GitHub 项目地址](https://github.com/jkjoy/cfmemos)
- [Memos 官方项目](https://github.com/usememos/memos)
- [Cloudflare Workers 文档](https://developers.cloudflare.com/workers/)
- [Cloudflare D1 文档](https://developers.cloudflare.com/d1/)
- [Cloudflare R2 文档](https://developers.cloudflare.com/r2/)