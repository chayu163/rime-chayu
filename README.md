# rime-chayu

茶鱼的个人 [Rime](https://rime.im) 配置，基底为[雾凇拼音 rime-ice](https://github.com/iDvel/rime-ice)。全拼单方案 + 中英混输，个人定制全部收敛在两个补丁文件中。

## 定制内容

- **方案**：仅雾凇拼音（全拼）；中英混输、简繁切换、`Uu` 部件反查、`V` 符号模式、`/rq` `/sj` 日期时间均为上游内置能力，通过 `default.custom.yaml` 裁定启用范围
- **配色**：8 套 `茶鱼·` 前缀方案——雾岭 / 墨玉 / 靛青 / 胭脂（半透明玻璃），象牙白 / 宋韵 / 翡翠（平实纸感），雪松（印石），定义于 `weasel.custom.yaml`
- **字体**：中文 苹方（PingFang SC，未装则回退思源黑体），拉丁与序号 Times New Roman
- **预览图**：`preview/` 下按方案 id 存放设定界面缩略图
- **设计稿**：`design/` 配色画布（浏览器打开），记录各方案的视觉依据与混搭思路

## 安装

前提：Windows + [小狼毫](https://rime.im/download/) 0.17.4+。

```powershell
git clone git@github.com:chayu163/rime-chayu.git "$env:APPDATA\Rime"
& "C:\Program Files\Rime\weasel-0.17.4\WeaselDeployer.exe" /deploy
```

克隆即得全部定制。配色可在小狼毫「输入法设定」中随时切换。

## 定制入口

只改以下两个文件，上游文件保持原样，更新时直接覆盖：

| 文件 | 职责 |
|---|---|
| `default.custom.yaml` | 行为：方案列表、候选数 |
| `weasel.custom.yaml` | 外观：配色定义、字体栈、激活方案 |

颜色格式为 `0xAABBGGRR`（透明度/蓝/绿/红），玻璃款半透明依赖 AA 通道。

## 致谢

词库、方案与 Lua 脚本均来自 [rime-ice](https://github.com/iDvel/rime-ice)，本仓库仅含个人定制层。
