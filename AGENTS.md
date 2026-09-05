# 仓库上下文（给 agent）

茶鱼的个人 Rime（小狼毫 0.17.4 / Windows）配置仓库，基底为雾凇拼音 rime-ice 上游。用户目录即本仓库根：`%APPDATA%\Rime`。GitHub：`chayu163/rime-chayu`（SSH 推送）。

## 文件地图

| 类别 | 文件 | 说明 |
|---|---|---|
| **个人定制（可改）** | `default.custom.yaml` | 方案列表、候选数 |
| | `weasel.custom.yaml` | 8 套配色、字体栈、激活方案 |
| | `preview/color_scheme_<id>.png` | 设定界面缩略图 |
| 上游原样（勿改） | `rime_ice.schema.yaml` `default.yaml` `weasel.yaml` `cn_dicts/` `en_dicts/` `lua/` `opencc/` 等 | 更新时整体覆盖 |

## 操作流程：改外观配置

1. 让用户**关闭小狼毫设定窗口**（开着会回写 `weasel.custom.yaml`，覆盖外部修改）
2. 修改补丁文件
3. `taskkill //IM WeaselDeployer.exe //F` 清掉单实例互斥，再执行 `"C:\Program Files\Rime\weasel-0.17.4\WeaselDeployer.exe" /deploy`
4. 部署是异步的，等 25 秒后查 `%APPDATA%\Rime\build\` 验证；完整重建词库可能耗时数分钟
5. 配色有增改时，同步重生成 `preview/` 缩略图（headless Chrome 在 `~/.cache/hyperframes/chrome`）

## 硬事实

- **Rime 颜色格式 `0xAABBGGRR`**（透明度/蓝/绿/红）：CSS `#RRGGBB` 换算时反转 R、B 两个字节；半透明只改 AA 通道，Weasel 透底无模糊
- **设定界面的配色列表在打开时刻读取**：先部署完成，再打开设定窗口
- **`rime_ice.userdb/` 是 WeaselServer 持锁的 leveldb 活数据库**：勿拷贝、勿入库；词频备份应走用户词典同步，但 `WeaselDeployer /sync` 实测无产物（源码 `configurator.SyncUserData()` 存在，原因未查明），已搁置
- 部署器/服务异常时先查进程：遗留的 WeaselDeployer 会让新部署静默失败
- 字体栈：`Times New Roman`（拉丁）→ `PingFang SC` → `Noto Sans SC`（中文回退）→ emoji 链，位于 `style/font_face`

## 提交规范

配置变更后 commit 并 push。**不入库**（.gitignore 已配）：`build/`、`installation.yaml`、`user.yaml`、`*.userdb/`。历史首个提交含 57.8MB 的 `build/rime_ice.table.bin`（GitHub 仅警告），如需瘦身需重写历史 + 强推。

## 本机环境

- 代理 `127.0.0.1:7897`，shell 命令用 `px` 包裹；Node 走 mise；默认 pwsh 7
- 历史设计稿：桌面 `小狼毫皮肤设计画布 v2.html`
