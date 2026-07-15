# uBlock Origin 与 Fuck Fuckadblock 的兼容性问题

## 问题概述

uBlock Origin (uBO) 用户尝试添加 Fuck Fuckadblock 过滤列表时，可能会发现列表无法正常工作——显示 "0 of 0 used filters"（使用了 0 条规则中的 0 条），列表实际上被静默禁用了。

## 根本原因

这是 uBlock Origin 团队**刻意为之**的行为。具体机制如下：

### 1. `badlists.txt` 黑名单机制

uBlock Origin 的 [uAssets](https://github.com/uBlockOrigin/uAssets) 仓库中维护了一个名为 [`badlists.txt`](https://github.com/uBlockOrigin/uAssets/blob/master/filters/badlists.txt) 的文件，其中列出了被禁止的第三方过滤列表 URL。

当 Fuck Fuckadblock 的 URL 被加入此文件后：

- 每次 uBO 检查过滤列表更新时，会自动下载最新的 `badlists.txt`
- 如果用户订阅的列表 URL 匹配 `badlists.txt` 中的条目，uBO 会**自动禁用**该列表的更新
- 用户**无法在 uBO 设置中关闭此行为**——`badlists.txt` 的更新是强制的

### 2. 列入黑名单的过程

Fuck Fuckadblock 被加入 `badlists.txt` 的过程：

- uAssets 仓库的提交 [c5d77a6](https://github.com/uBlockOrigin/uAssets/commit/c5d77a625c7c130d665110ba0672d7007dbda6dc) 和 [35a3a37](https://github.com/uBlockOrigin/uAssets/commit/35a3a373023842c3fd61cb1b8d521d64762d0171)
- 相关 PR：[uAssets #18161](https://github.com/uBlockOrigin/uAssets/pull/18161)
- uBO 团队成员 `mapx-` 是执行此操作的负责人

### 3. 为什么这是审查行为

1. **用户无选择权**：uBO 不提供选项让用户选择是否信任某个第三方列表
2. **无法禁用**：用户无法关闭 `badlists.txt` 的自动更新
3. **缺乏透明度**：大多数用户不知道他们的列表被静默禁用了
4. **单方面决定**：少数几个人决定数百万用户不能使用哪些列表

## 解决方案

有以下几种方法可以绕过此限制：

### 方法一：阻止 `badlists.txt` 的下载

通过在系统层面（hosts 文件、防火墙或使用 AdGuard 等工具）阻止 uBO 下载 `badlists.txt`。

**需要阻止的 URL：**
```
https://raw.githubusercontent.com/uBlockOrigin/uAssets/master/filters/badlists.txt
```

**使用 hosts 文件（Linux/macOS）：**
```
127.0.0.1 raw.githubusercontent.com uBlockOrigin
```

> ⚠️ 注意：此方法会阻止对所有 `raw.githubusercontent.com` 上 uBlockOrigin 资源的访问，可能会影响 uBO 自身的过滤列表更新。更精确的方法是使用 AdGuard 等工具进行 URL 级别的拦截。

**使用 AdGuard：**
在 AdGuard 中添加用户规则，阻止：
```
||raw.githubusercontent.com/uBlockOrigin/uAssets/master/filters/badlists.txt^
```

### 方法二：在 URL 后添加随机参数

在订阅链接后面添加一个无意义的查询参数，使 URL 与 `badlists.txt` 中的条目不匹配：

```
https://raw.githubusercontent.com/grill-glitch/fuckfuckadblock/master/fuckfuckadblock.txt?_=3
```

> ℹ️ 这是一种简单有效的绕过方式。uBO 的 `badlists.txt` 匹配的是精确 URL，添加任何查询参数都会使 URL 不匹配。

### 方法三：使用 CDN 镜像

使用不同的 CDN URL 来订阅列表，这些 URL 不在 `badlists.txt` 中：

反广告屏蔽绕过：
```
https://fuckfuckadblock.pages.dev/fuckfuckadblock.txt
https://raw.githack.com/grill-glitch/fuckfuckadblock/master/fuckfuckadblock.txt
https://cdn.statically.io/gh/grill-glitch/fuckfuckadblock/master/fuckfuckadblock.txt
```

挖矿屏蔽：
```
https://fuckfuckadblock.pages.dev/fuckfuckadblock-mining.txt
https://raw.githack.com/grill-glitch/fuckfuckadblock/master/fuckfuckadblock-mining.txt
https://cdn.statically.io/gh/grill-glitch/fuckfuckadblock/master/fuckfuckadblock-mining.txt
```

### 方法四：切换到 AdGuard

**最推荐的长期解决方案。** AdGuard 不会对第三方过滤列表进行这种审查，你可以自由订阅任何你信任的列表。

AdGuard 在功能上与 uBlock Origin 相当，并且在某些方面（如元素选择器、脚本注入等）甚至更为强大。

## 为什么 uBO 团队要封禁此列表

官方理由是"列表质量问题"或"规则冲突"，但实际情况更为复杂：

1. **维护者间的个人冲突**：Fuck Fuckadblock 作者与 uAssets 维护者之间存在长期矛盾
2. **规则风格差异**：FFA 使用了一些被 uBO 团队认为"不够优雅"的规则写法
3. **缺乏沟通**：uAssets 团队在封禁前没有与 FFA 作者进行充分沟通

无论理由如何，**剥夺用户选择权**的做法本身就值得商榷。开源精神的核心之一就是让用户自己做决定。

## 参考链接

- [原始 Issue - Banlist abuse #423](https://github.com/bogachenko/fuckfuckadblock/issues/423)
- [Reddit 讨论 - Abuse of the banlist](https://www.reddit.com/r/uBlockOrigin/comments/111wlyu/abuse_of_the_banlist/)
- [uAssets badlists.txt](https://github.com/uBlockOrigin/uAssets/blob/master/filters/badlists.txt)
- [uAssets PR #18161 - Update FFA block](https://github.com/uBlockOrigin/uAssets/pull/18161)
