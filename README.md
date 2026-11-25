# Syntec CNC Macro Maintenance Framework

一个通用的 CNC 宏程序维护方法框架，供 AI Agent 使用。

## 包含

- 宏程序盘点、功能识别、修改、自检、交付的标准流程；
- 通用宏语法（调用、引数、变量、单位、控制流、`G31`、报警）；
- 变量空间与寄存器规划（`#`/`@`/`R` 映射、参数镜像、间接寻址、刀表基址、变量台账）；
- 单位/精度/公英制换算（`Pr17` LIU、`Pr3241`、`G70/G71`、长度/速度换算、计数系数）；
- 按内容指纹识别功能、找同功能孪生；
- 改动同步矩阵与交付检查清单；
- 接入自有 Wiki/MCP 做 L2 校验的流程；
- 一个纯合成示例。

## 不包含

- 任何厂商内部文档、页面 ID、内部议题号或下载链接；
- 任何客户名称、项目名称、现场 BUG、人员姓名或内部版本号；
- 具体参数语义表、报警号分配表、机型差异表；只保留通用地址空间与映射方法。

这些内容属于各自组织/厂商的内部资料，需另行授权并在私有知识源中维护。

## 安装

把本目录放到你的 Agent skills 目录，例如：

```text
~/.codebuddy/skills/syntec-cnc-macro-framework/
~/.claude/skills/syntec-cnc-macro-framework/
~/.codex/skills/syntec-cnc-macro-framework/
```

目录名可自定；本仓库使用 `syntec-cnc-macro-framework`。也可以把 `SKILL.md` 作为系统提示，`references/` 作为按需读取的资料。

## 使用

1. 先读 `SKILL.md` 定流程；
2. 按 `references/macro-core.md` 第一部分给宏打功能标签；
3. 按 `references/macro-core.md` 第三部分规划变量与寄存器；
4. 按 `references/change-playbook.md` 第一部分列同步项；
5. 按 `references/change-playbook.md` 第二部分自检；
6. 需要规格校验时，按 `references/l2-access.md` 接你自己的知识源。

## 许可

本框架可查看、学习与内部使用；不附带任何第三方文档、客户数据或厂商内部资料的授权。
