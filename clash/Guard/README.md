## 说明

本目录三个规则文件（Advertising / Privacy / Hijacking）已于 2026-09 弃用并清空：

- 上游 DivineEngine/Profiles 已在 GitHub 删库（404），本地快照失去维护来源；
- 静态清单无法跟进广告/劫持域名轮换，宽关键字匹配（如 `adservice`）会误杀正常主机。

请改用持续更新的 rule-provider 订阅（二选一或组合，均为每日更新）：

```yaml
rule-providers:
  reject-ads:
    type: http
    behavior: classical
    format: yaml
    url: "https://cdn.jsdelivr.net/gh/blackmatrix7/ios_rule_script@master/rule/Clash/Advertising/Advertising_Classical.yaml"
    path: ./ruleset/bm7-advertising.yaml
    interval: 86400
  # 轻量替代（中文区命中率优先，behavior 为 domain）：
  #   url: "https://anti-ad.net/clash.yaml"

rules:
  # 如需保留浏览器钓鱼/恶意软件告警，放开下面一行（必须置于 REJECT 之前）：
  # - DOMAIN,safebrowsing.googleapis.com,DIRECT
  - RULE-SET,reject-ads,REJECT
```

说明：

- blackmatrix7 Advertising 已内含 Hijacking / Privacy / AdvertisingLite 子规则，一份即可整体替代本目录；
- 大陆直连环境拉取 GitHub raw 可能失败，建议使用 jsdelivr / ghproxy 镜像；
- 两源数据有重叠，同时订阅不影响正确性，只增加少量去重开销；
- 误拦截排查：mihomo 面板按策略 REJECT 过滤连接日志，找到误杀域名后在其前面加 exact 放行规则。
