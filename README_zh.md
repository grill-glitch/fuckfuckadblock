# Fuck Fuckadblock

用于屏蔽挖矿脚本、弹窗以及反广告屏蔽绕过的过滤规则列表。

本项目是 [bogachenko/fuckfuckadblock](https://github.com/bogachenko/fuckfuckadblock) 的复刻（fork）。上游仓库已于 2025 年 5 月 5 日归档，本复刻继续维护和更新过滤规则。

## 功能

- **反广告屏蔽绕过**：屏蔽网站检测广告拦截器并弹出警告的行为
- **弹窗屏蔽**：屏蔽各种弹窗和弹出式广告
- **挖矿脚本屏蔽**：屏蔽基于浏览器的加密货币挖矿脚本

## 使用方法

### 添加反广告屏蔽绕过 + 弹窗屏蔽列表

点击此按钮订阅 — [订阅](https://subscribe.adblockplus.org/?location=https://raw.githubusercontent.com/grill-glitch/fuckfuckadblock/master/fuckfuckadblock.txt&title=Fuck%20Fuckadblock)

或手动添加 RAW 链接：
```
https://raw.githubusercontent.com/grill-glitch/fuckfuckadblock/master/fuckfuckadblock.txt
```

### 添加挖矿脚本屏蔽列表

点击此按钮订阅 — [订阅](https://subscribe.adblockplus.org?location=https://raw.githubusercontent.com/grill-glitch/fuckfuckadblock/master/fuckfuckadblock-mining.txt&title=Fuck%20Fuckadblock%3A%20Mining)

或手动添加 RAW 链接：
```
https://raw.githubusercontent.com/grill-glitch/fuckfuckadblock/master/fuckfuckadblock-mining.txt
```

## CDN 镜像

反广告屏蔽绕过列表：

1. `https://fuckfuckadblock.pages.dev/fuckfuckadblock.txt`
2. `https://raw.githack.com/grill-glitch/fuckfuckadblock/master/fuckfuckadblock.txt`
3. `https://cdn.statically.io/gh/grill-glitch/fuckfuckadblock/master/fuckfuckadblock.txt`

挖矿屏蔽列表：

1. `https://fuckfuckadblock.pages.dev/fuckfuckadblock-mining.txt`
2. `https://raw.githack.com/grill-glitch/fuckfuckadblock/master/fuckfuckadblock-mining.txt`
3. `https://cdn.statically.io/gh/grill-glitch/fuckfuckadblock/master/fuckfuckadblock-mining.txt`

## 关于 uBlock Origin 的问题

> [!WARNING]
> **uBlock Origin 用户可能无法正常添加本列表。** 这是因为 uBlock Origin 团队将本过滤列表加入了其内部黑名单（`badlists.txt`），导致 uBO 会自动禁用本列表的更新。

### 原因

uBlock Origin 的 `uAssets` 仓库维护了一个名为 `badlists.txt` 的文件，其中包含被禁止的过滤列表 URL。一旦某个列表被加入此文件，uBlock Origin 会在每次更新过滤规则时自动禁用该列表。这本质上是一种**审查行为**——uBO 团队单方面决定用户不能使用哪些第三方列表。

相关讨论详见：
- [Banlist abuse · Issue #423](https://github.com/bogachenko/fuckfuckadblock/issues/423)
- [Reddit: Abuse of the banlist](https://www.reddit.com/r/uBlockOrigin/comments/111wlyu/abuse_of_the_banlist/)
- [uAssets PR #18161](https://github.com/uBlockOrigin/uAssets/pull/18161)

### 解决方案

详细的绕过方法和说明请参阅 [docs/ublock-origin-issues.md](docs/ublock-origin-issues.md)。

### 推荐替代方案

如果你对 uBlock Origin 的这种行为感到不满，可以考虑使用 **AdGuard**——它不会审查第三方过滤列表，可以正常订阅和使用本列表。

## 反馈问题

如果你发现网站的反广告屏蔽检测未被拦截，或者本列表导致了网站功能异常，请提交 Issue：

- [报告反广告屏蔽绕过](https://github.com/grill-glitch/fuckfuckadblock/issues/new?template=adblock-bypass.md)
- [报告网站功能异常](https://github.com/grill-glitch/fuckfuckadblock/issues/new?template=broken-bypass.md)
- [报告弹窗绕过](https://github.com/grill-glitch/fuckfuckadblock/issues/new?template=popup-bypass.md)
- [报告挖矿脚本绕过](https://github.com/grill-glitch/fuckfuckadblock/issues/new?template=miner-bypass.md)

## 许可证

MIT License

---

本项目原始作者为 Bogachenko Vyacheslav，上游仓库地址：[bogachenko/fuckfuckadblock](https://github.com/bogachenko/fuckfuckadblock)
