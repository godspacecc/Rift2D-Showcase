# Rift2D

[English](README.md) | [中文](README_CN.md)

Rift2D 是一个 Unity 2D 项目，当前目标是搭建“大厅准备、地图探索、资源回收、结算成长”的核心玩法闭环，并验证最小实时联机同步链路。

仓库当前重点是小规模可玩闭环和长期可维护性：在明确的业务流程中沉淀 QFramework 风格分层、UI 管理、资源加载、配置表、热更新、编辑器工具、本地联机服务和自动化测试。

## 当前能力

- **Unity 2D 主流程**：`Boot`、`Lobby`、`Dungeon` 场景组成当前启动、大厅、副本和回大厅流程。
- **QFramework 风格分层**：用 Model / System / Command / Controller / Event 拆分状态、业务规则、流程编排和 Unity 接入。
- **多存档槽**：支持存档列表、读档、删档和开始界面继续游戏入口。
- **资源与配置管线**：使用 YooAsset 管理资源加载，使用 Luban XML / CSV 生成运行时配置。
- **代码热更新边界**：保留开发期外部 DLL 热重载，并接入 HybridCLR 发布期 `Game` 热更程序集，`Boot` 作为稳定宿主程序集。
- **最小实时联机**：本地 TCP realtime server 支持加入唯一房间、房主开始副本、玩家快照同步、移动输入同步和玩家离开广播。
- **项目工具链**：包含 UI 生成、资源引用诊断、动画诊断、场景切换、YooAsset 打包、本地化和服务器发布辅助工具。
- **自动化验证**：通过 Unity EditMode 测试、.NET server tests 和 headless TCP smoke test 覆盖关键契约。

## 技术栈

- Unity 2022.3
- C#
- QFramework 风格 MVC / Command / Event 架构
- UGUI / TextMeshPro
- Unity Test Framework
- YooAsset
- Luban
- HybridCLR
- TCP + proto3 realtime protocol

## 仓库结构

```text
F:\GitHub\Rift2D\
|-- AGENTS.md             # Codex / 项目协作规则
|-- README.md             # 项目概览
|-- docs\                 # 知识库：规范、流程、系统、工具、决策
|-- Tools\                # 仓库级工具、生成器、脚本、本地服务
`-- Rift2D\               # Unity Hub 打开的 Unity 项目目录
    |-- Assets\           # Unity 资源、场景、脚本和编辑器扩展
    |-- Packages\         # Unity package manifest / lock
    `-- ProjectSettings\  # Unity 项目设置
```

仓库级工具放在根目录 `Tools/`，不直接放进 Unity 工程：

```text
Tools/
|-- Hotfix/                  # 开发期外部 DLL 热重载工程
|-- Luban/                   # 配置表定义、数据源和生成脚本
|-- RealtimeProtocol/        # realtime proto 定义
|-- RealtimeServer/          # 本地实时服务
|-- RealtimeServer.Tests/    # 实时服务测试
|-- RealtimeSmokeTest/       # 双客户端 TCP smoke test
|-- start_realtime_server.bat
|-- start_lan_test_servers.bat
`-- start_yooasset_local_server.bat
```

## Unity 项目结构

Unity 工程资源主要放在 `Rift2D/Assets/`：

```text
Rift2D/Assets/
|-- AssetBundleCollectorSetting.asset # YooAsset 资源收集配置
|-- Editor/                           # Unity Editor 工具和菜单
|-- Game/                             # 当前游戏主资源与运行时代码
|-- GameHotUpdate/                    # HybridCLR 发布期热更程序集
|-- HybridCLRGenerate/                # HybridCLR 生成代码和 link.xml
|-- Scenes/                           # Unity 默认/示例场景目录，不进入当前主流程构建
|-- Settings/                         # URP 等渲染配置
|-- StreamingAssets/                  # 客户端配置和首包资源构建输出
|-- Tests/                            # Unity EditMode 测试
`-- TextMesh Pro/                     # TMP 导入资源
```

`Rift2D/Assets/Game/Scripts/` 按职责分层：

```text
Command/      # 一次性流程编排
Controller/   # Unity 场景、Prefab、UI 和输入接入
Framework/    # 项目内框架基础代码
Model/        # 业务状态和配置数据
Network/      # 实时通信协议、传输、分发和同步
Query/        # 只读查询封装
Save/         # 存档数据结构
System/       # 长期业务规则和系统协调
ThirdParty/   # 第三方生成或适配代码
Utility/      # 资源加载、UI、热重载等通用工具
```

## 开发约定

- 业务状态放在 Model。
- 长期业务规则放在 System。
- 一次性流程编排放在 Command。
- Unity 场景、Prefab、UI 和输入接入放在 Controller。
- DTO 停留在网络边界，进入业务 Model 后转换为项目内状态对象。
- 自动化验证优先使用 EditMode 测试、server tests 和 headless smoke test。

## 当前目标

围绕 2D 核心玩法闭环持续完善大厅、副本、结算、资源管线、工具链、热更新和测试覆盖；联机方向保持最小可验证闭环，优先稳定协议边界、房间流程和本地/局域网验证方式。
