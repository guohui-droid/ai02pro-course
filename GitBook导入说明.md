# 把课程文档导入 GitBook —— 操作说明

已为你把 12 份 Word 实验指导书全部转换为 **GitBook 最兼容的 Markdown 格式**（含图片资源），组织为：

```
AI02pro实验课程/
├── README.md                       ← 课程主页（含全部文档链接）
├── 01-基础理论/                     ← 章节：基础理论
│   ├── 大语言模型基础.md (+ _assets/)
│   ├── 机器视觉基础.md (+ _assets/)
│   └── 知识库介绍.md
├── 02-AI02pro操作与实验/            ← 章节：操作与实验（7 篇实验指导书）
└── 03-PQVistaPro/                  ← 章节：工具软件
```

**为什么不用网页版 Import pages？** 单次导入最多 20 个页面 + 20 个附件，而这套资料共 12 页、**259 张图片**，网页导入必然超限；且 Word 直接导入会丢失格式。所以推荐走 Git Sync（官方针对大量内容的标准方案，无数量限制）。

---

## 方案一（推荐）：Git Sync 全量同步

总耗时约 10 分钟，一次同步后以后更新内容只需 push 仓库。

### 第 1 步：在 GitHub 建仓库（不用上传文件）

1. 打开 https://github.com/new
2. Repository name 填 `ai02pro-course`（可自定义）
3. 选 **Private 或 Public** 均可，**不要**勾选 "Add a README"、"Add .gitignore"、"Choose a license"（保持空仓库）
4. 点 Create repository

### 第 2 步：本地推送到 GitHub

在终端执行（把 `<你的GitHub用户名>` 换成实际的）：

```bash
cd "/Users/guohui/WorkBuddy/2026-09-01-14-33-52/AI02pro实验课程"
git init
git add .
git commit -m "AI02pro 实验课程文档（12 篇指导书）"
git branch -M main
git remote add origin https://github.com/<你的GitHub用户名>/ai02pro-course.git
git push -u origin main
```

> 提示：Mac 上首次 push 会弹出 GitHub 登录窗口（浏览器），登录授权即可；或到 GitHub → Settings → Developer settings → Personal access tokens 生成 token，用 `https://<用户名>:<token>@github.com/...` 方式推送。

### 第 3 步：GitBook 连接仓库同步

1. 打开你的 Space：https://app.gitbook.com/o/TaMVQ5myh85jAVdgWjQK/s/TDHxiO4RGnKTQCHeuNb6/
2. 左侧目录把内容先清空（或直接用空 Space 开始）
3. 点左下角 **Space Settings（齿轮）→ Git Sync**
4. **Install GitHub Sync**（按引导授权你的 GitHub 账号，选择刚建的 `ai02pro-course` 仓库）
5. 同步方向选择 **GitHub → GitBook**
6. 保存后 GitBook 会自动把仓库内容拉进来，目录结构自动变成：
   - `01-基础理论`（分组）→ 3 个页面
   - `02-AI02pro操作与实验`（分组）→ 7 个页面
   - `03-PQVistaPro`（分组）→ 2 个页面
   - 根目录 README.md → 课程主页
7. 进入你之前那个 change request，点 **Merge** → **Publish**，公开链接生成，发给学生即可

### 以后更新内容

在本地改 .md → `git add . && git commit -m "更新" && git push`，GitBook 自动同步。

---

## 方案二：网页逐篇导入（无 GitHub 场景）

每篇文档单独导入（每篇图片数需 ≤ 20 才稳妥）：

1. 左侧目录 → **Add new → Import pages**
2. 选择 **Markdown**，上传某个章节的单个 `.md` 文件（如 `大语言模型基础.md`）
3. GitBook 会自动把同目录 `_assets/` 里的图片一起识别吗？**不会** —— 需先手动在页面上传图片，或用方案一

> 结论：这套资料有 259 张图片，**强烈建议方案一**。若不便用 GitHub，可以告诉我，我把每篇文档按「图片 ≤ 20 张」拆包，你逐篇导入。

---

## 转换说明（给需要重复操作的人）

环境：macOS 自带 pandoc 3.8（`/opt/anaconda3/bin/pandoc`）

```bash
# Word → Markdown（图片提取到 <文件名>_assets/）
pandoc 指导书.docx -t gfm --extract-media="指导书_assets" --wrap=none -o 指导书.md
```

转换后需做一次 GitBook 兼容后处理（HTML img 标签 → Markdown 图片语法、嵌入视频引用 → 提示行），已由脚本完成。

> 注意：`知识库介绍.docx` 内嵌引用了一个视频文件「CHL-AI-02Pro-人工智能大模型实验箱.mp4」，docx 里只有链接没有实体文件，导入后需单独上传该视频（找设备厂商要源文件）。
