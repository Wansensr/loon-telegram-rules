# loon-telegram-rules

Loon 规则订阅：Telegram（kelee.one 原文件的镜像）+ 1 条本地新增。

## 订阅地址

主地址：

```
https://raw.githubusercontent.com/Wansensr/loon-telegram-rules/main/Telegram.lsr
```

`raw.githubusercontent.com` 连不上时用 jsDelivr（钉死 commit，避免 CDN 缓存滞后）：

```
https://cdn.jsdelivr.net/gh/Wansensr/loon-telegram-rules@6497cf6/Telegram.lsr
```

## 与上游的差异

- 上游 40 条**逐条未动、顺序未动**，原文副本见 [`original/`](original/)，sha256 `8a8bbf11b9852deeb7f4edd56ae61125eae3115af86329481ba028e7d077d60d`。
- 新增 **1 条**，放在文件最前面：

```
DOMAIN-SUFFIX, iturrit.com
```

- 为什么加：Turrit（第三方 Telegram 客户端）的消息流量是裸 IP 连 Telegram 数据中心，本来就命中本规则集；但它自己的接口 `api.iturrit.com` 不带任何 Telegram 特征，实测落到配置末尾的 `FINAL`，也就是另一个策略组（🇺🇸 DD49-EB2中转）。加上这条，接口和消息才走同一个策略组。
- 头注释改过（引用链接 / 本仓库 / 这 1 条新增的说明），注释不参与匹配。

## 添加

Loon → 配置 → 规则 → 右上角 `+` → 添加订阅规则 → 粘贴上面任一地址 → 策略组选你的 Telegram 组（如 `Telergram`）。

## 注意

- **不要和 kelee 原订阅 `https://rule.kelee.one/Loon/Telegram.lsr` 同时启用**，同一批规则会重复。切换时先删旧的再加新的。
- 本仓库是快照，**不会自动跟上游更新**。上游若有改动，需要重新拉取并 diff 一次。
- 规则里的策略名不写在文件里，由 Loon 添加订阅时指定的策略组决定，所以换节点不影响本文件。

## 来源与校验

- 上游：`https://rule.kelee.one/Loon/Telegram.lsr`。该站对非浏览器客户端返回 Cloudflare 403，原文取自 GitHub 镜像 `mihoyo-typ/KeleeOne`（`Rule/Telegram.lsr`，文件头 `# 引用链接` 指向同一 URL）。
- 上游快照：`2025-09-18 02:34:42，RuleCount：40`，UTF-8 无 BOM，副本已入库。
- 本文件：41 条（40 上游 + 1 新增），UTF-8 无 BOM，LF 换行。

## 版本记录

- **v1**（2026-10-20）：建仓。上游 40 条原样搬运，新增 `DOMAIN-SUFFIX, iturrit.com`。