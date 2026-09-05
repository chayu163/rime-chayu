# 仓库上下文（给 agent）

茶鱼的个人 Rime（小狼毫）配置仓库，基底为雾凇拼音 rime-ice 上游。用户目录 `%APPDATA%\Rime`，机器名 CHAYU。

## 核心原则：补丁哲学

**永不修改上游文件**。所有个人定制收敛在两个文件里，上游更新时直接覆盖上游文件即可：

- `default.custom.yaml` — 行为：schema_list（仅 rime_ice）、候选数 6
- `weasel.custom.yaml` — 外观：8 套 `茶鱼·` 配色、字体栈、激活方案

## 关键事实（踩过的坑）

- **小狼毫设定界面会回写 `weasel.custom.yaml`**：窗口开着时会用下拉框状态覆盖 `style/color_scheme`，且可能冲掉并发修改。改此文件前让用户关闭设定窗口，改完重新部署
- **Rime 颜色格式是 `0xAABBGGRR`**（透明度/蓝/绿/红，BGR 字节序），从 CSS `#RRGGBB` 换算要反转 R/B
- **半透明靠 back_color 的 AA 通道**，Weasel 只做 Alpha 透底、无模糊
- **`rime_ice.userdb/` 是运行中的 leveldb 活数据库**，被 WeaselServer 锁定，勿动勿入库；词频备份的正确路径是用户词典同步（功能尚未调通，已搁置）
- **部署**：`WeaselDeployer.exe /deploy`（先 taskkill 遗留的 WeaselDeployer，否则单实例互斥导致静默失败）；完整重建词库可能耗时数分钟
- **`/sync` 参数存在但调不通**：源码有 `configurator.SyncUserData()`，实际运行无产物，原因未查明，已搁置
- 设定界面的配色列表在**打开时刻**读取，部署完成后再打开才能看到新方案
- **预览图**：`preview/color_scheme_<scheme_id>.png`，用 headless Chrome（`~/.cache/hyperframes/chrome`）按配色真实渲染生成，改配色后需同步更新

## 字体栈

`Times New Roman`（拉丁）→ `PingFang SC` → `Noto Sans SC`（中文，苹方未装时回退）→ emoji 链。写在 `weasel.custom.yaml` 的 `style/font_face`。

## 提交规范

配置变更后 commit；**不入库**：`build/`、`installation.yaml`、`user.yaml`、`*.userdb/`（见 .gitignore）。远程 `origin = git@github.com:chayu163/rime-chayu.git`（SSH，账号 chayu163）。

## 本机环境

- Windows + 小狼毫 0.17.4，代理走 `127.0.0.1:7897`（shell 命令用 `px` 包裹），Node 用 mise
- 设计画布（历史方案）：桌面 `小狼毫皮肤设计画布 v2.html`
