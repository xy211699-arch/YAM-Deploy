# 2026-10-09 工作流初始化

- 状态：通过（工作流文件静态检查；不代表实验阶段验收）
- 范围：轻量仓库工作流和模板；不是 P1～P6 的实验执行。
- 执行位置：原开发电脑的新目录 `/home/joe/project/YAM-Deploy`。

## 交付内容

保留用户指定的目录，补充 `.gitignore`。提供六阶段任务与 Codex 提示、环境保护规则、现场状态交接、可替换模型配置和统一报告模板。

GitHub 元数据确认目标仓库 `xy211699-arch/YAM-Deploy` 为 private，初始化前为空且具备写权限。模型保持暂定；实验室版本、路径和标定信息留待现场核实。

## 验证记录

在上述本地目录，用现有 RoboTwin Python 环境的标准库和 PyYAML 执行一次只读静态检查，未安装新依赖：

| 检查 | 结果 |
|---|---|
| 目录与交付文件 | 12 个文件，符合约定目录 |
| Markdown 相对链接、代码块、行尾 | 无错误 |
| 配置 YAML | 解析通过；模型未选定、现场未确认、动作输出关闭 |
| 任务清单 | 六阶段共 18 项，编号唯一，均未勾选 |
| 常见凭据模式 | 未发现匹配；另经人工检查无实际凭据 |

这是文档与配置检查，不是自动测试套件。没有运行模型、训练、VR 或实机测试。发布后的文件一致性由交付时 GitHub 回读核对，提交历史保留发布证据。

## 下一步

在实验室主机执行 P1.1，只读盘点现有 EVA/VR 链路。先使用 README 的启动提示，不直接运行公开仓库默认硬件启动器。

## 来源

- [EVA-CLIENT](https://github.com/Noietch/EVA-CLIENT)：截至本次查看，公开 main 为 `e02d04e44a89c5c37bb94c4b2ee1a4521f2848a2`；仅作参考，不代表实验室工作版本。
- [YAM 硬件说明](https://github.com/Noietch/EVA-CLIENT/blob/e02d04e44a89c5c37bb94c4b2ee1a4521f2848a2/examples/hardware/yam/README.md)：独立环境与启动副作用。
- [EVA 记录格式](https://github.com/Noietch/EVA-CLIENT/blob/e02d04e44a89c5c37bb94c4b2ee1a4521f2848a2/docs/recording.md)：按实际版本检查数据字段与存储行为。
- [Codex AGENTS.md](https://developers.openai.com/codex/guides/agents-md)：仓库工作指令。

没有修改原 Lingbot-yam 工程、实验室环境、设备配置或任何运行中的服务。
