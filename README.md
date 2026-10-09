# YAM-Deploy

在实验室 4090 主机上，用 **YAM 双臂工作站 + EVA-CLIENT VR 数据采集 + 可替换的策略模型**，跑通一个 pick-and-place 最小闭环。

本仓库提供给 Codex 持续执行的工作流、配置模板与实验记录。初始版本尚未实现模型适配器，也未在实验室主机完成环境、训练或部署验收。LingBot-VLA-v2 是暂定模型，不是项目固定依赖。

## 从这里开始

将仓库放到实验室主机的新目录，在该目录打开 Codex，发送：

> 阅读 AGENTS.md、docs/STATUS.md 和 docs/TODO.md。先执行 P1.1 的只读盘点，确认实验室实际 EVA/VR 工程、环境和启动方式，记录原目录中的本地修改。不要启动硬件或改动原环境。完成后更新进度、给出证据和下一步；只询问阻塞当前任务的信息。

后续每次使用：

> 按 AGENTS.md，从 STATUS 指定的下一项继续。先核对本项前置条件，在授权范围内完成实施和验证，更新报告、TODO 和 STATUS。不要跳过验收，也不要把未运行的检查标为通过。

当前机器不是实验室主机时，可以整理文档和开发离线代码；现场阶段保持待验证。

## 六个阶段

| 阶段 | 完成时应得到什么 |
|---|---|
| P1 硬件连接 | 已保存现场基线，并确认原 YAM + VR 链路可用 |
| P2 环境搭建 | 新模型环境可单独使用，原 EVA/硬件环境仍可恢复和使用 |
| P3 模型离线测试 | 合成或录制观测 → 模型 → 经过检查的动作，不下发实机 |
| P4 数据采集 | VR 示教经过质检，形成固定的数据集和训练/验证划分 |
| P5 模型训练 | 短训练和正式微调完成，导出的模型可重新加载 |
| P6 模型部署 | 经现场验收后完成固定回合评测，保存成功数和失败记录 |

具体动作、验收与下一条 Codex 指令集中在 [TODO](docs/TODO.md)。P4 的真实数据需要回到 P3 复核接口；P6 的失败可反馈到采集/训练，不改变原始实验记录。

## 系统分工

```text
采集：VR → EVA 的重定向/IK → 已验证的 YAM 执行节点 → 机械臂
                          └→ 同步保存图像、状态、实际目标动作

部署：相机和关节反馈 → EVA → 模型适配器 → 本机模型服务
                         ← 检查过的动作块 ←
      EVA → 原 YAM 执行节点 → 机械臂
```

原 EVA 客户端、硬件节点和新增模型环境保持隔离。复用现场配置，不复制公开示例中的序列号、标定值、零位和启动动作。模型服务不直接打开 CAN。

## 仓库内容

```text
YAM-Deploy/
├── AGENTS.md
├── README.md
├── .gitignore
├── docs/
│   ├── SPEC.md
│   ├── DECISIONS.md
│   ├── STATUS.md
│   └── TODO.md
├── experiments/
│   ├── configs/project.example.yaml
│   └── reports/TEMPLATE.md
├── tests/README.md
└── version_history/README.md
```

复制 `experiments/configs/project.example.yaml` 为同目录 `project.local.yaml`，按盘点结果填写。它是配置记录模板，不是已经接入运行器的可执行配置；禁止猜值补齐。

原始数据、视频、权重、依赖环境放在仓库外。仓库只提交脱敏配置、轻量报告、测试样本以及后续必要代码。需要适配器或脚本时再创建 `src/`、`scripts/`，不预先堆空目录。

## 怎样判断项目跑通

从一个已记录的数据版本训练出模型，在相同工作站重新加载，通过受限实机验收，完成固定条件的 pick-and-place 评测。记录成功数/总数、人工干预和基础设施异常。

没有预设保证成功率。候选模型、数据数量和评测门槛应在相应阶段确定并记录。

## 参考

- [EVA-CLIENT](https://github.com/Noietch/EVA-CLIENT)：保留实验室已经验证的 VR 路径。
- [LingBot-VLA-v2](https://github.com/Robbyant/lingbot-vla-v2)：暂定模型，后续可以替换。
- [Codex AGENTS.md](https://developers.openai.com/codex/guides/agents-md)：项目指令机制。

文档是工作约定，不能代替设备权限隔离和现场急停。
