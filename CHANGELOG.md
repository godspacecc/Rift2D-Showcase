# Rift2D 更新日志

所有重要的项目变更都会记录在此文件中。

格式基于 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/)。

[English](CHANGELOG_EN.md) | [中文](CHANGELOG.md)

---

## [未发布]

### 新增
- 无

### 变更
- 无

### 修复
- 无

---

## [0.1.0] - 2026-06-25

首个版本，核心系统基础搭建完成。

### 新增
- **项目架构**：Unity 2022.3 + QFramework 风格分层（Model/System/Command/Controller/Event）
- **场景流程**：启动 → 大厅 → 地下城 → 返回大厅，完整游戏循环骨架
- **存档系统**：多存档槽支持，创建/加载/继续/删除存档
- **背包系统**：背包原型，物品栏基础结构
- **资源管线**：YooAsset 资源加载管道，支持本地/远程资源
- **配置系统**：Luban XML/CSV 配置表工作流
- **热更新边界**：HybridCLR 集成，Boot（宿主）与 Game（热更）程序集分离
- **多人联机**：最小实时多人验证路径，TCP 协议，本地/LAN 测试支持
- **工具链**：
  - UI 生成工具
  - 资源引用诊断
  - 动画诊断
  - YooAsset 打包辅助
  - 本地化辅助
  - 服务器发布辅助
- **自动化验证**：Unity EditMode 测试、.NET server tests、headless TCP smoke test
- **展示仓库**：GitHub Actions 自动同步文档和 Release 到展示仓库

### 变更
- 无

### 修复
- 无

[未发布]: https://github.com/godspacecc/Rift2D-Showcase/compare/v0.1.0...HEAD
[0.1.0]: https://github.com/godspacecc/Rift2D-Showcase/releases/tag/v0.1.0