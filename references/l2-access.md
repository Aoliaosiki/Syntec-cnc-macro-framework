# 接入你自己的 Wiki/MCP 做 L2 校验

> 本文是通用流程，不含任何公司站点、cloudId、空间名或页面 ID。把 `<...>` 换成你自己的环境。
> 本文件只公开接入、探测与降级流程；具体站点、页面 ID、空间权限和全量索引留在私有知识库。
> 探测失败不阻塞本地盘点：按 L1 继续做文件、语法、单位与变量检查，并在结论里标注“云端校验未完成”。

## 一、L2 的判定标准

只要求两件事实际成功返回：

| 能力 | 最小验证 |
|---|---|
| 搜索 | 用 CQL/关键词能返回页面 id |
| 读页 | 按 id/URL 能返回正文与 `version`/`lastModified` |

“能登录”不算 L2；必须有工具返回。

## 二、标准四步

### 1. 探搜索

```text
search(query='id = <known-page-id>', limit=1)
```

- 返回 1 条 → 搜索可用；
- 返回 0 条但无报错 → 页面不可见或 id 错，改用 `space = "<space>" AND title ~ "<keyword>"`；
- 报错/tool not found → 降级 L1。

### 2. 探读页

```text
get_page(content_id='<known-page-id>', format='markdown', detail='summary')
```

- 有 `version` + `lastModified` → L2 解锁；
- 无版本 → 受限 L2，记录“版本不可得”；
- 401/403/404/超时 → 按降级阶梯处理。

### 3. 按主题精读

1. 功能词 + 特征 token 组查询；
2. 候选页先看标题/更新时间；
3. 规格/验收页读全文；现场页只记结论；
4. 至少交叉“最新规格 + 最近验收”两页。

### 4. 记录与回写

```text
| page id | version / lastModified | 校验项 | 结论 |
```

本地回写：补规则（带来源）、更新索引状态、规格页变更时刷新快照、冲突保留双方。

## 三、客户端适配

工具名按能力找，不按名字找。

| 客户端 | 接入 | 常见工具名 |
|---|---|---|
| Codex | 运行环境注入 MCP | `mcp__<server>__search` / `get_page` |
| Claude Code/Desktop | MCP 设置加 remote MCP（SSE/HTTP），OAuth 后重启会话 | `mcp__<server>__*` |
| CodeBuddy | MCP/插件设置加连接器 | 可能不带前缀，按 `tools/list` |
| WorkBuddy | 连接器/知识源 | 可能是通用 `search`/`fetch` |

只有通用 `search`/`fetch` 时：`search` 传查询语句，`fetch` 传页面 URL；不要假设通用搜索支持 CQL。

## 四、降级阶梯

| 情况 | 判定 | 做法 |
|---|---|---|
| search + get 成功且有版本 | L2 | 正常校验 |
| get 成功但无版本 | 受限 L2 | 可核对文字，不能写“最新” |
| 只有 search 成功 | L1+ | 只能确认页面存在 |
| 401/403 | L1 | 重新授权一次；仍失败标“无权限” |
| 404 | L1 | 查 id/空间，不要猜 |
| 超时/网络失败 | L1 | 重试一次后标“网络失败” |
| tool not found | L1 | 客户端未配置 MCP |

## 五、安全

- 凭据由客户端管理，禁止写进技能文件、脚本或对话。
- 禁止用 `curl` 携带 Cookie/Token 抓 HTML 代替 MCP。
- 禁止猜页面 id、猜空间、猜 URL。
- 未校验就写 `云端校验：未完成`，不要用“应该/通常”补规格。
