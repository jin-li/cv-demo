# 锦鲤简历演示站点

本仓库演示如何使用 [锦鲤简历](https://github.com/jin-li/jinli-cv) Hugo 主题创建一个美观、可打印的多语言简历网站。

**在线演示：** [https://jinli-cv-demo.netlify.app/](https://jinli-cv-demo.netlify.app/)

## 概述

本仓库展示了如何：
- 将锦鲤简历主题作为 Git 子模块使用
- 配置多个 CV 版本（不同语言/版本）
- 自定义内容、样式和部署
- 部署到 Netlify（或任何静态托管服务）

实际的 CV 内容和配置来自主题的 `exampleSite/` 目录，该目录直接从主题子模块中提供。

## 仓库结构

```
cv-demo/
├── themes/
│   └── jinli-cv/          # 锦鲤简历主题 (git 子模块)
│       ├── exampleSite/   # <- 这是实际被服务的内容
│       │   ├── config.toml
│       │   ├── content/
│       │   ├── data/
│       │   └── static/
│       └── ...            # 主题源代码
├── netlify.toml           # Netlify 构建配置
├── .gitmodules            # 子模块定义
└── README.md              # 说明文档
```

## 🚀 工作原理

本仓库不包含自己的内容。相反：
1. `锦鲤简历` 主题作为 Git 子模块包含在内
2. Netlify 从 `themes/jinli-cv/exampleSite/` 构建网站（在 `netlify.toml` 中指定）
3. 主题的示例站点提供了一个完整的、可用的 CV 演示，包括：
   - 默认 CV（主页）
   - 德语版本 (`/cv-de/`)
   - 中文版本 (`/cv-zh/`)
   - 所有板块的示例数据（经验、项目、出版物等）

## 🔧 自定义您的个人 CV

基于本演示创建一个您自己的个性化 CV 网站：

### 选项 1：Fork 并自定义（推荐）
1. **Fork** 本仓库到您的 GitHub 账户
2. **自定义内容：**
   - 编辑 `themes/jinli-cv/exampleSite/data/content.yaml`（默认 CV）
   - 修改/添加语言版本 `themes/jinli-cv/exampleSite/data/cv-*/`
   - 用您的照片替换 `themes/jinli-cv/exampleSite/static/img/avatar.png`
   - 在 `themes/jinli-cv/exampleSite/config.toml` 中调整颜色、字体和布局
3. **推送到 GitHub** - Netlify 将自动重新构建并部署您的更改

### 选项 2：从头创建仓库
1. 创建一个新仓库
2. 将锦鲤简历主题添加为子模块：
   ```bash
   hugo new site my-cv-site
   cd my-cv-site
   git init
   git submodule add https://github.com/jin-li/jinli-cv.git themes/jinli-cv
   cp -r themes/jinli-cv/exampleSite/* .
   ```
3. 创建主题软链接：
   ```bash
   mkdir -p themes
   ln -s ../../.. themes/jinli-cv
   ```
4. 自定义内容（与选项 1 相同）
5. 添加 `netlify.toml`（见下文）
6. 推送到 GitHub 并连接到 Netlify

## 🛠️ 本地开发

预览本地更改：

### 使用主题的 exampleSite（推荐用于测试）
```bash
# 克隆锦鲤简历主题
git clone https://github.com/jin-li/jinli-cv.git
cd jinli-cv/exampleSite

# 创建指向主题的软链接（本地开发需要）
mkdir -p themes
ln -s ../.. themes/jinli-cv

# 启动开发服务器
hugo server -D
```
访问 http://localhost:1313/

### 使用您自己的仓库
```bash
hugo server -D
```

## ⚙️ Netlify 部署

本仓库通过 `netlify.toml` 配置为 Netlify 自动部署：

```toml
[build]
  base = "themes/jinli-cv/exampleSite"
  command = "hugo"
  publish = "public"

[build.environment]
  HUGO_VERSION = "0.146.5"
```

**重要：** `base` 设置告诉 Netlify 从主题的 exampleSite 目录中运行构建命令，此目录包含实际的 `config.toml`、`content/` 和 `data/` 目录。

### 手动 Netlify 设置
如果通过 Netlify UI 连接：
1. **构建命令**：`hugo`
2. **发布目录**：`public`
3. **构建环境变量**：`HUGO_VERSION = 0.146.5`
4. **重要**：确保基础目录设置正确（如果使用 `netlify.toml` 则可以留空）

## 📝 自定义指南

### 内容文件
所有内容都是 YAML/TOML 格式，位于 `data/` 目录：
- `data/content.yaml` - 默认 CV（主页）
- `data/cv-de/config.toml` + `data/cv-de/content.yaml` - 德语版本
- `data/cv-zh/config.toml` + `data/cv-zh/content.yaml` - 中文版本

### 可自定义的主要板块
- **个人信息**：姓名、职称、头像、联系方式
- **个人简介**：专业摘要/个人介绍
- **工作经验**：工作历史、描述和技能标签
- **教育背景**：学位、学校、相关课程
- **项目经验**：个人/专业项目详情和技能标签
- **出版物**：研究论文、文章、演示文稿
- **论文**：学术论文/学位论文详情
- **技能**：技术技能、语言等
- **语言**：语言熟练程度
- **个人兴趣**：爱好、个人兴趣
- **证书**：认证、许可证、奖项

### 样式与布局
在 `themes/jinli-cv/exampleSite/config.toml` 中修改：
- 颜色：`colorPrimary`、`colorDark`、`colorLight` 等
- 布局：`section_order`、`side_section_order`
- 各板块样式：边距、填充、间距
- 功能开关：`showDownload`、`download_button` 位置

## 🖨️ 打印与 PDF 导出

CV 针对 A4 打印进行了优化：
1. 在浏览器中打开您的 CV
2. 按 `Ctrl+P`（Mac 为 `Cmd+P`）
3. 设置：
   - **纸张大小**：A4
   - **页边距**：无/默认（内置 0.5cm 上下页边距）
   - **缩放**：100%
   - **背景图形**：**启用**（徽标/渐变色需要）
4. 点击"另存为 PDF"或"打印"

## 📄 许可证

本演示站点按原样提供，用于教育目的。锦鲤简历主题采用 MIT 许可证 - 详见 [LICENSE](LICENSE) 文件和 [锦鲤简历仓库](https://github.com/jin-li/jinli-cv/blob/main/LICENSE)。

## 🙏 致谢

- **原始主题**：[Almeida CV](https://github.com/ineesalmeida/almeida-cv) 由 Inês Almeida 创作 (MIT 许可证)
- **当前主题**：[锦鲤简历](https://github.com/jin-li/jinli-cv) 由 Jin Li 维护 (MIT 许可证)
- **演示数据**：仅用于演示目的的示例数据

---

*最后更新：2026 年 7 月*