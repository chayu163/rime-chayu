# rime-chayu · 茶鱼的 Rime 配置

基于 [雾凇拼音 rime-ice](https://github.com/iDvel/rime-ice) 的个人定制配置。单方案极简路线：全拼 + 中英混输，只维护两个补丁文件。

## 特性

- **单方案**：只启用雾凇拼音（全拼），中英混输由内置的 melt_eng 提供，无双拼/五笔干扰
- **8 套自设计配色**：`茶鱼·` 前缀命名，4 款半透明玻璃（雾岭/墨玉/靛青/胭脂）+ 3 款纸感平实（象牙白/宋韵/翡翠）+ 雪松印石，深浅色可跟随系统
- **字体方案**：中文 苹方 → 思源黑体回退；拼音/英文/序号 Times New Roman
- **反查与符号**：`Uu` 部件反查、`V` 模式符号、`/rq` `/sj` 日期时间、简繁切换

## 安装

前提：[小狼毫](https://rime.im/download/) Weasel 0.17.4+。

```powershell
git clone git@github.com:chayu163/rime-chayu.git "$env:APPDATA\Rime"
```

右键托盘小狼毫图标 →「重新部署」，或运行：

```powershell
& "C:\Program Files\Rime\weasel-0.17.4\WeaselDeployer.exe" /deploy
```

> 字体：装有苹方（PingFang SC）时中文自动使用；未装则回退到思源黑体（Noto Sans SC）。

## 定制入口

**只改两个文件，永不改上游**（上游更新直接覆盖）：

| 文件 | 管什么 |
|---|---|
| `default.custom.yaml` | 行为：方案列表、候选数 |
| `weasel.custom.yaml` | 外观：配色、字体、激活方案 |

配色为 Rime 颜色格式 `0xAABBGGRR`（透明度/蓝/绿/红），玻璃款靠 AA 通道半透明。设定界面（托盘 → 输入法设定）可随时切换配色，选择会写回 `weasel.custom.yaml`。

## 仓库管理规范

- **入库**：配置源文件、`preview/`（设定界面预览缩略图）
- **不入库**：`build/`（部署产物）、`installation.yaml`、`user.yaml`、`*.userdb/`（运行时被锁的活数据库）

## 致谢

词库、方案、Lua 脚本均来自 [rime-ice](https://github.com/iDvel/rime-ice)，本仓库仅含个人定制层。
