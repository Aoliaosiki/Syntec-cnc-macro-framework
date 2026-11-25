# 更新记录

版本遵循 SemVer。版本号以 `VERSION` 为唯一来源，构建时同步写入 `BUILD-INFO.json`、README 标题与徽章。

## v0.1.0 — 2026-11-25

首个公开版本。

### 新增

- `SKILL.md`：五条原则、L1/L2/L3 能力分级、五步标准工作流、同步项与输出约定
- `references/macro-core.md`：功能指纹、宏语法与调用、`#`/`@`/`R` 变量空间、扩充参数读取路径、`G31`、控制流、单位与公英制
- `references/change-playbook.md`：同步矩阵、改动前/中/后检查清单、备份与交付目录
- `references/l2-access.md`：自有 Wiki/MCP 接入、L2 判定、客户端适配与降级阶梯
- `examples/example-macro.md`：纯合成对刀宏骨架
- `VERSION` 与 `BUILD-INFO.json`：版本号与构建校验结果
- `SANITIZATION-REPORT.md`：公开版脱敏说明与自检记录

### 校验

- `SKILL.md` frontmatter 与目录名一致
- `references/`、`examples/` 引用完整，Markdown 表格无结构问题
- 无绝对路径、内部页面 ID、客户名、零宽字符、BOM
- denylist、pageIdScan、absolutePathScan 全部通过

### 说明

- 公开版只含通用方法与公开语法，不含厂商内部页面、客户项目、参数/报警号表
- 具体机型规格需接入使用者自有知识源，并在结论中标注能力级别
