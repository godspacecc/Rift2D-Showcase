# 同步设置指南

本文档说明如何在开发仓库配置 GitHub Actions 自动同步到展示仓库。

---

## 同步内容

| 内容 | 触发方式 | 说明 |
|------|----------|------|
| 文档（README/CHANGELOG/ROADMAP） | 自动触发 | 修改文档并 push 时自动同步 |
| Release | 自动触发 | 开发仓库发布 Release 时自动同步到展示仓库 |
| Release Assets | 自动同步 | 构建产物随 Release 自动同步 |

---

## 触发方式

### 文档同步

当以下文件变化并 push 到 `main` 分支时，自动同步：
- `README.md` / `README_EN.md`
- `CHANGELOG.md` / `CHANGELOG_EN.md`
- `ROADMAP.md` / `ROADMAP_EN.md`
- `screenshots/` 目录下的文件

### Release 同步

当开发仓库发布 Release 时，自动同步 Release 信息和 assets 到展示仓库。

---

## Release 发布流程

### 自动发布（推荐）

使用发布脚本一键完成构建、打包、发布：

```bash
cd E:/UnityProject/Rift2D/Tools
publish.bat v0.1.0 zip
```

脚本自动执行：
1. Unity 命令行构建
2. 打包压缩（支持 zip/rar/7z）
3. 创建 GitHub Release 并上传
4. 自动同步到展示仓库

### 手动发布（备选）

如果脚本不可用，可以手动操作：

#### 1. 本地构建

在 Unity Editor 中执行：
```
菜单 → Tools → 打包 → 1. Build
```

构建产物位于：`Builds/Windows_IL2CPP/`

#### 2. 打包发布

将构建产物打包为压缩文件（支持 zip、rar、7z 等格式）：
```
Builds/Windows_IL2CPP/ → Rift2D-v0.1.0-Windows.zip
```

#### 3. 创建 Release

在开发仓库创建 Release：
https://github.com/godspacecc/Rift2D/releases/new

- **Tag**: 填写版本号（如 `v0.1.0`）
- **Title**: 填写标题
- **Notes**: 从 CHANGELOG 复制该版本的更新内容
- **Assets**: 上传打包的构建产物（zip 文件）

#### 4. 自动同步

创建 Release 后，工作流自动触发：
- Release 信息同步到展示仓库
- Assets 同步到展示仓库的 Release

---

## 工作流文件

| 文件 | 说明 |
|------|------|
| `sync-to-showcase.yml` | 文档同步 |
| `sync-release.yml` | Release 同步 |

## 前置条件

- 开发仓库和展示仓库都在 GitHub 上
- 您对两个仓库都有管理权限

---

## 设置步骤

### 1. 创建 Personal Access Token (PAT)

1. 访问 GitHub → Settings → Developer settings → Personal access tokens → Fine-grained tokens
2. 点击 **Generate new token**
3. 配置：
   - **Token name**: `Rift2D Showcase Sync`
   - **Expiration**: 选择合适的有效期（建议 1 年）
   - **Repository access**: Only select repositories → 选择 `Rift2D-Showcase`
   - **Permissions** → Repository permissions:
     - Contents: Read and write
     - Metadata: Read
4. 点击 **Generate token**
5. **立即复制并保存 Token**（只显示一次）

### 2. 在开发仓库添加 Secret

1. 打开开发仓库 → Settings → Secrets and variables → Actions
2. 点击 **New repository secret**
3. 配置：
   - **Name**: `SHOWCASE_REPO_TOKEN`
   - **Secret**: 粘贴上一步创建的 PAT
4. 点击 **Add secret**

### 3. 复制工作流文件到开发仓库

将 `sync-to-showcase.yml` 复制到开发仓库的 `.github/workflows/` 目录。

### 4. 修改工作流配置（可选）

编辑 `sync-to-showcase.yml`，根据实际情况修改：

```yaml
env:
  SHOWCASE_REPO: godspacecc/Rift2D-Showcase  # 展示仓库地址
  SHOWCASE_BRANCH: main                        # 展示仓库分支
```

---

## 使用方法

### 手动触发同步

1. 打开开发仓库 → Actions → Sync to Showcase
2. 点击 **Run workflow**
3. 配置参数：
   - **version**: 发布版本号（如 `v0.1.0`），留空则跳过发布
   - **update_readme**: 是否更新 README
   - **update_changelog**: 是否更新 CHANGELOG
   - **update_roadmap**: 是否更新 ROADMAP
4. 点击 **Run workflow**

### 自动触发（可选）

如需在特定事件后自动同步，可在工作流中添加触发条件：

```yaml
on:
  workflow_dispatch:  # 手动触发
  push:
    branches: [main]
    paths:
      - 'README.md'
      - 'CHANGELOG.md'
      - 'ROADMAP.md'
```

---

## 文件结构要求

开发仓库应包含以下文件（会同步到展示仓库）：

```
dev-repo/
├── README.md          # 英文说明
├── README_CN.md       # 中文说明（可选）
├── CHANGELOG.md       # 更新日志
├── ROADMAP.md         # 英文路线图
├── ROADMAP_CN.md      # 中文路线图（可选）
└── screenshots/       # 截图目录（可选）
```

---

## 故障排除

### Token 权限错误

确保 PAT 有正确的权限：
- Contents: Read and write
- Repository access 包含展示仓库

### 工作流未触发

- 检查工作流文件是否在正确的分支
- 确认 Actions 已在仓库设置中启用

### Release 创建失败

- 检查版本号是否已存在
- 确保 CHANGELOG.md 格式正确

---

## 注意事项

- 同步会覆盖展示仓库中的对应文件
- 建议在开发仓库维护主文档，展示仓库仅作为镜像
- 截图需要手动放入开发仓库的 `screenshots/` 目录