# DMIT 香港套餐：三条线路怎么选，Tier 1 / Eyeball / Premium 配置与价格对比（附全套餐价格表）

搜「DMIT 香港套餐」的人，十个里有八个卡在同一个地方：官网购物车一打开，左边是 region、generation、network 三个筛选器，右边一排 HKG.AS3.T1、HKG.AS3.EB、HKG.AN5.Pro 之类的名字，价格从年付 36.9 美元一路排到月付 759.9 美元。名字长得像乱码，差价比配置差得还大。

这篇就把这件事拆开：香港机房三条网络到底差在哪，每条线下面有哪些套餐、多少钱，以及哪些隐藏限制会在你付完钱之后才冒出来。

## 先搞清楚：香港机房的三个 network 是不同的线路，不是不同的硬件

DMIT 香港节点部署在 Equinix HK2，官方把香港产品按网络质量分成三档，购物车里的 `network` 筛选器对应的就是这三档：

- **Tier 1（T1）**：纯国际路由，接 RETN、NTT 这类国际骨干，官方明确说明**不针对中国大陆做优化**。优势是端口大（4–10Gbps）、流量多、单价低，香港到欧洲的延迟表现好。
- **Eyeball（EB）**：定位在 T1 和 Premium 中间。官方描述是「结合 Tier 1 国际传输 + 面向中国大陆的 best-effort 路由」，也就是尽力而为，不承诺线路质量。
- **Premium（Pro）**：旗舰。电信方向去程 CN2 GIA 直连香港 CTG、回程同样走 CN2 GIA；联通走 AS4837 + AS10099；移动走香港 CMI 直连。这一档才是真正为大陆访问付钱的地方。

另外购物车里的 `generation` 是硬件代际：**AS3 是 AMD EPYC 7003 系列，AN5 是 AMD EPYC 9005 系列**（部分资料提到 AN5 配 DDR5 内存）。同一档网络可能同时存在两种平台，价格不一样，这也是很多人看价格表看得一头雾水的原因。

一句话判断：**你的用户在不在中国大陆，决定你买哪一档；你的业务吃不吃单核性能，决定你买 AS3 还是 AN5。**

## 三条线路横向对比

| 线路 | 中国大陆优化 | 典型端口 | 超量后行为 | 起价 |
| --- | --- | --- | --- | --- |
| Tier 1（HKG.AS3.T1） | 无 | 4–10Gbps | 降速继续跑，不限量 | $36.9/年（WEE） |
| Eyeball（HKG.AS3/AN5.EB） | 尽力而为（Beta） | 500Mbps–1Gbps | 暂停 | $39.9/月 |
| Premium（HKG.AS3/AN5.Pro） | CN2 GIA + CMI + AS4837 | 1Gbps | 暂停 | $39.9/月 |

测试 IP 可以拿来自己摸底再下单：Premium 常用 103.117.100.199，T1 常用 154.12.176.28，官方还提供 Looking Glass 供路由追踪。延迟受你本地运营商和时段影响很大，别人的测速图只能当参考。

## 香港 Tier 1 全套餐价格表（HKG.AS3.T1）

EPYC 7003 平台，国际线路，1 IPv4 + 1 IPv6 /64。流量按进出取最大值计，用完之后不关机，降速继续用，这一点比很多同类产品厚道。

| 套餐 | CPU | 内存 | 硬盘 | 月流量 / 端口 | 价格 | 购买 |
| --- | --- | --- | --- | --- | --- | --- |
| WEE | 1 核 | 1GB | 20GB SSD | 1TB / 4Gbps（超量限速 50Mbps） | $36.90 / 年 | [查看 WEE 套餐](https://www.dmit.io/aff.php?aff=12046) |
| TINY | 1 核 | 1GB | 20GB SSD | 2TB / 4Gbps（限速 100Mbps） | $6.90 / 月 | [查看 TINY 套餐](https://www.dmit.io/aff.php?aff=12046) |
| STARTER | 1 核 | 2GB | 40GB SSD | 4TB / 10Gbps（限速 100Mbps） | $12.90 / 月 | [查看 STARTER 套餐](https://www.dmit.io/aff.php?aff=12046) |
| MINI | 2 核 | 2GB | 60GB SSD | 8TB / 10Gbps（限速 100Mbps） | $21.90 / 月 | [查看 MINI 套餐](https://www.dmit.io/aff.php?aff=12046) |
| MICRO | 4 核 | 4GB | 80GB SSD | 16TB / 10Gbps（限速 200Mbps） | $32.90 / 月 | [查看 MICRO 套餐](https://www.dmit.io/aff.php?aff=12046) |
| MEDIUM | 4 核 | 8GB | 160GB SSD | 32TB / 10Gbps（限速 200Mbps） | $49.90 / 月 | [查看 MEDIUM 套餐](https://www.dmit.io/aff.php?aff=12046) |
| LARGE | 8 核 | 16GB | 320GB SSD | 64TB / 10Gbps（限速 500Mbps） | $99.90 / 月 | [查看 LARGE 套餐](https://www.dmit.io/aff.php?aff=12046) |
| GIANT | 8 核 | 24GB | 640GB SSD | 128TB / 10Gbps（限速 1Gbps） | $199.90 / 月 | [查看 GIANT 套餐](https://www.dmit.io/aff.php?aff=12046) |

T1 里最值的是 WEE：36.9 美元一年，1TB 流量，超了限速 50Mbps 继续跑，拿来放个静态站、做中转落地、或者当香港出口都很够用。缺点也很直白——电信联通访问大概率绕路，延迟可能比美西还难看。这条线是给「要香港 IP、但不服务大陆用户」的人准备的。

## 香港 Eyeball 全套餐价格表（HKG.EB）

官方目前仍把香港 Eyeball 标记为 **Beta**，页面写明「不建议用于对稳定性要求较高的生产环境」。线路会调整，库存也一直是断断续续的状态。

**AS3 平台（EPYC 7003）**

| 套餐 | CPU | 内存 | 硬盘 | 月流量 / 端口 | 价格 | 购买 |
| --- | --- | --- | --- | --- | --- | --- |
| WEE | 1 核 | 1GB | 20GB SSD | 500GB / 500Mbps | $24.90 / 月 | [查看 EB WEE](https://www.dmit.io/aff.php?aff=12046) |
| TINY | 1 核 | 1GB | 20GB SSD | 800GB / 1Gbps | $39.90 / 月 | [查看 EB TINY](https://www.dmit.io/aff.php?aff=12046) |
| STARTER | 1 核 | 2GB | 40GB SSD | 1.5TB / 1Gbps | $79.90 / 月 | [查看 EB STARTER](https://www.dmit.io/aff.php?aff=12046) |
| MINI | 2 核 | 4GB | 60GB SSD | 2.2TB / 1Gbps | $126.90 / 月 | [查看 EB MINI](https://www.dmit.io/aff.php?aff=12046) |
| MICRO | 4 核 | 4GB | 80GB SSD | 3TB / 1Gbps | $179.90 / 月 | [查看 EB MICRO](https://www.dmit.io/aff.php?aff=12046) |
| MEDIUM | 4 核 | 8GB | 160GB SSD | 4TB / 1Gbps | $239.90 / 月 | [查看 EB MEDIUM](https://www.dmit.io/aff.php?aff=12046) |

**AN5 平台（EPYC 9005，配 DDR5）**

| 套餐 | CPU | 内存 | 硬盘 | 月流量 / 端口 | 价格 | 购买 |
| --- | --- | --- | --- | --- | --- | --- |
| MINI | 4 核 | 4GB | 80GB SSD | 2.2TB / 1Gbps | $149.90 / 月 | [查看 AN5 EB MINI](https://www.dmit.io/aff.php?aff=12046) |
| MICRO | 4 核 | 4GB | 160GB SSD | 3TB / 1Gbps | $199.90 / 月 | [查看 AN5 EB MICRO](https://www.dmit.io/aff.php?aff=12046) |
| MEDIUM | 6 核 | 8GB | 160GB SSD | 4TB / 1Gbps | $279.90 / 月 | [查看 AN5 EB MEDIUM](https://www.dmit.io/aff.php?aff=12046) |
| LARGE | 8 核 | 16GB | 320GB SSD | 4.5TB / 1Gbps | $359.90 / 月 | [查看 AN5 EB LARGE](https://www.dmit.io/aff.php?aff=12046) |
| GIANT | 12 核 | 24GB | 640GB SSD | 9TB / 1Gbps | $759.90 / 月 | [查看 AN5 EB GIANT](https://www.dmit.io/aff.php?aff=12046) |

同价位下 EB 的流量通常比 Pro 多出约六成，代价是路由保证低一档：电信去程走 CN2、联通和移动去程没做优化，回程是联通 CUG + CMI 动态负载、移动 CMI、电信 163。移动用户体感会明显好于电信联通。

## 香港 Premium 全套餐价格表（HKG.Pro，CN2 GIA）

这条线才是「香港 + 大陆低延迟」这个需求的答案。电信双向 CN2 GIA、联通 AS4837 + AS10099、移动香港 CMI，第三方测评里大陆三网平均延迟普遍报告在 40ms 上下，晚高峰会有波动但幅度不大——注意这是别人测出来的数字，不是承诺值。

**AS3 平台（EPYC 7003）**

| 套餐 | CPU | 内存 | 硬盘 | 月流量 / 端口 | 价格 | 购买 |
| --- | --- | --- | --- | --- | --- | --- |
| TINY | 1 核 | 1GB | 20GB SSD | 500GB / 1Gbps | $39.90 / 月 | [查看 Pro TINY](https://www.dmit.io/aff.php?aff=12046) |
| STARTER | 1 核 | 2GB | 40GB SSD | 1000GB / 1Gbps | $79.90 / 月 | [查看 Pro STARTER](https://www.dmit.io/aff.php?aff=12046) |
| MINI | 2 核 | 2GB | 60GB SSD | 1500GB / 1Gbps | $126.90 / 月 | [查看 Pro MINI](https://www.dmit.io/aff.php?aff=12046) |
| MICRO | 2 核 | 4GB | 80GB SSD | 2000GB / 1Gbps | $179.90 / 月 | [查看 Pro MICRO](https://www.dmit.io/aff.php?aff=12046) |
| MEDIUM | 4 核 | 4GB | 160GB SSD | 2500GB / 1Gbps | $239.90 / 月 | [查看 Pro MEDIUM](https://www.dmit.io/aff.php?aff=12046) |

**AN5 平台（EPYC 9005）**——官网已把 Pro 常规产品迁到 AN5，价格与同档 AS3 基本对齐，部分档位硬盘更大。

| 套餐 | CPU | 内存 | 硬盘 | 月流量 / 端口 | 价格 | 购买 |
| --- | --- | --- | --- | --- | --- | --- |
| MINI | 4 核 | 4GB | 80GB SSD | 1500GB / 1Gbps | $149.90 / 月 | [查看 AN5 Pro MINI](https://www.dmit.io/aff.php?aff=12046) |
| MICRO | 4 核 | 4GB | 160GB SSD | 2000GB / 1Gbps | $199.90 / 月 | [查看 AN5 Pro MICRO](https://www.dmit.io/aff.php?aff=12046) |
| MEDIUM | 6 核 | 8GB | 160GB SSD | 2500GB / 1Gbps | $279.90 / 月 | [查看 AN5 Pro MEDIUM](https://www.dmit.io/aff.php?aff=12046) |
| LARGE | 8 核 | 16GB | 320GB SSD | 3000GB / 1Gbps | $359.90 / 月 | [查看 AN5 Pro LARGE](https://www.dmit.io/aff.php?aff=12046) |
| GIANT | 12 核 | 24GB | 640GB SSD | 6000GB / 1Gbps | $759.90 / 月 | [查看 AN5 Pro GIANT](https://www.dmit.io/aff.php?aff=12046) |

> DMIT 的库存和硬件代际切换很频繁，香港常年处于「售罄—补货—再售罄」的循环里。上表是按公开页面整理的当前档位，下单前请以购物车实时显示的配置和价格为准。

## 价格表之外，几个容易踩的点

**超量后的处理方式完全不同。** T1 用超流量是降速继续跑，WEE 降到 50Mbps、大配置能保到 1Gbps，服务不停。Pro 和 EB 用的是另一套逻辑，超量直接暂停虚拟实例。如果你跑的是下载站、镜像站、或者流量很难预估的业务，这个差别比月租差价重要得多。

**Eyeball 的 Beta 标签不是装饰。** 官方自己说了路由和性能可能继续调整，也说了不建议放在对稳定性要求高的生产环境。看到 EB 比 Pro 便宜一大截就冲，然后发现晚高峰路由变了，这种事在第三方社区里并不少见。

**Pro 正在从 AS3 换到 AN5。** 对买家来说，同一档套餐可能有两个平台版本、两个价格。下单时看清楚 generation 筛选器选的是哪个，别只看套餐名。

**Epic 级别的配置不一定值。** MEDIUM 往上，价格涨得比流量快。GIANT 的 759.9 美元月付对绝大多数业务都是浪费，除非你确实需要 12 核 24GB 加 6TB 流量。

## 关于优惠码，现在的真实情况

第三方站点上流传着一堆 DMIT 优惠码，格式大多类似 `_HKG_..._RECURRING`，特点是**只对季付及以上生效、属于循环折扣（续费也打折）**，而且经常带库存和时效限制。同时也有多个较新的渠道明确写着「本次补货已是特价，暂无有效优惠码」。

这两件事不矛盾：DMIT 的补货本身就是促销价，优惠码通常针对特定产品线和付款周期，用完即止。

所以实际操作建议是：先选好套餐和付款周期，在结账页面把看到的优惠码填进去点验证，能减就减，减不了就按原价买——不要因为一个过期的码去改自己的付款周期或产品线。别为了省几十美元买一条你根本用不上的线路。

## 按需求选：四个具体场景

**只要一个香港 IP，用户主要在国外** → T1 的 WEE（$36.9/年）或 TINY（$6.9/月）。别买 Pro，白花钱。

**移动用户为主，预算有限但要求能连国内** → Eyeball 的 AS3 TINY 或 WEE。回程 CMI 对移动友好，价格比 Pro 低一档。接受 Beta 标签带来的不确定性。

**面向大陆用户建站、跑业务后台，延迟就是命** → Pro。TINY（$39.9/月）起步试水，流量吃紧再上 STARTER。这是 DMIT 香港套餐里最有明确购买理由的一档。

**CPU 密集型业务，比如数据库、API 网关、编译类任务** → 优先看 AN5 平台的 Pro 或 EB，Zen 5 架构配 DDR5，单核性能比 7003 平台强，多花的那点钱在这里是有回报的。

## 购买和支付

DMIT 支持支付宝、微信支付、PayPal 和信用卡，对国内用户来说下单环节没什么门槛。需要留意的是，官方已经把独立的中文支持团队取消了，工单统一走英文，遇到问题用英文沟通效率更高。

另外，DMIT 的香港货量本身不大，补货节奏也不规律。如果你已经确定要买，选好套餐直接下单比等下一轮补货更实在。

👉 [对照官网购物车挑选你的香港套餐](https://www.dmit.io/aff.php?aff=12046)

## 常见问题

**DMIT 香港套餐最低多少钱？**
目前能买到的最低门槛是 Tier 1 的 WEE，年付 36.90 美元。月付最低是 T1 的 TINY，6.90 美元/月。

**Tier 1 真的不能用来服务大陆用户吗？**
官方说明是不针对中国大陆做优化。实际表现因运营商和地区而异，移动偶尔还能接受，电信联通普遍绕路。如果你的收入依赖大陆访问体验，不要赌这条路。

**Eyeball 和 Premium 差价值不值？**
看你的用户在哪。如果大陆访问是核心指标，Pro 的 CN2 GIA 双向直连和 EB 的 best-effort 不是一个量级的东西，差价买的是路由确定性。如果用户主要是移动网络或者流量需求很大，EB 的流量额度更有吸引力。

**香港 Premium 会不会一直缺货？**
会周期性缺货。DMIT 香港的库存历来紧张，补货后往往很快售罄，这也是为什么很多人把它当限量品在蹲。

**能不能只用 IPv6？**
不能。香港全系默认给 1 个 IPv4 加 1 个 /64 IPv6，不是二选一。

最后一句实话：DMIT 香港套餐的价格在同配置里不算便宜，同价位你完全能买到核数和内存翻倍的别家产品。你付的这笔钱买的是香港机房位置、CN2 GIA 这条线路，以及一个不超售的承诺。如果这三样里有任何一样对你的业务不重要，那这套套餐就不适合你。
