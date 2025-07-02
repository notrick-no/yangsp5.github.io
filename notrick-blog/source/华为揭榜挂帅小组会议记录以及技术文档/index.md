---
title: 华为揭榜挂帅小组会议记录以及技术文档
date: 2025-07-02 21:50:56
---
# 会议记录

## 6.30

大家集中读题（代金券500）

分享对于知识蒸馏和强化学习的理解

给大家看看目前环境配置的成果

- CANN（Cuda），nnal+二进制算子包 （cudnn）（配置环境变量）
- 规格：Ascend: 1*ascend-snt9b1（32GB）|ARM: 24核 192GB
- 模型：qwen2.5-3B
- 推理框架：vllm、vllm-ascend

接下来要做什么（A榜不做筛选，B榜才筛人）

- **6.30-7.7 (模型蒸馏实现)**
- **7.7-7.14（****强化学习****实现）**
- **7.15-7.20（优化，打榜A）**
- 7.20-8.12（优化推理速度（算子融合开发and so on））

安排分工（大家暑假什么安排，是否需要调整）

- 模型蒸馏组（苏思远、张硕）
- 强化学习调参组（李特、方瑜）
- 读论文读项目组（俞凡）qwen3，deepseek-v3，每一次会议至少分享一个项目的思路or技术细节

协同工作方案

-    方案一：代码发给我我来运行。
-    方案二：挂载文件夹＋ssh免密连接。
-    方案三：todesk远程控制我电脑，我电脑连服务器。

老师资源

支，无服务器，有一块测端开发板，算子相关知识

王，模型蒸馏、强化学习

辛立明，？

**下次开会时间周四20:00**

## 6.31

- 解决远程连接的问题

接下来要做的事情：

1. 看比赛提交要求，能不能用外部服务器跑让后迁移到昇腾环境
2. 了解技术**黑盒蒸馏**、**白盒蒸馏**
3. 复现群里的论文，关注模型蒸馏的实现
4. 看看有没有支持昇腾的开源的蒸馏框架
5. 了解一下多卡训练、参数并行，模型并行
6. 分布式计算框架

参考链接：

【1】要复现的论文：https://github.com/microsoft/LMOps/tree/main/minillm

【2】通过 torch-npu 库完成了对华为昇腾 910b 系列芯片的支持, 包含 32GB 和 64GB 两个版本：https://llamafactory.readthedocs.io/zh-cn/latest/advanced/npu.htmlLLaMA-Factory 

【3】快速了解知识蒸馏的基本逻辑：https://www.bilibili.com/video/BV1gS4y1k7vj/?spm_id_from=333.337.search-card.all.click

【4】大模型蒸馏，黑盒白盒：https://zhuanlan.zhihu.com/p/706214065

【5】知识蒸馏的三个基本算法：https://cloud.tencent.com/developer/article/2203297

# 技术文档

## VScode remote 连接服务器

问题描述：window下用vscode 远程连接昇腾服务器，**mac****环境用以下方法会有问题**，有待解决。

技术实现：

【确定vscode的版本】

​     vscode版本要求为1.85，下载链接https://code.visualstudio.com/updates/v1_85

​     可以先跳过这个步骤，如果后来连不上服务器再换vscode的版本。

【安装扩展Remote - SSH】

![img](https://wcn9wp389ugs.feishu.cn/space/api/box/stream/download/asynccode/?code=MDhhMjAyMGU1YmYyMjE0N2RlMjhkMDRjMDE2MDJlOTZfR0M5TnVXeHRtV0ZYbGZCUGVyWFd2OGw2alFHVGtqSEhfVG9rZW46VU85SWJhMnBnb1JyRkp4YURreGNsSkRKbjdkXzE3NTE0NjQxNjA6MTc1MTQ2Nzc2MF9WNA)

【下载群里的密钥】

![img](https://wcn9wp389ugs.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDhlNjJhNjc1MjE0OGQyNDkyY2UzNDc0YTRlODI1ZGJfWmpGeGthWkJHajdyTjVsVnBJN3puZG04RHNibTdSTHBfVG9rZW46WGdKUGJGRlBxbzg2emZ4dXRRZmNqRjZTbnd1XzE3NTE0NjQxNjA6MTc1MTQ2Nzc2MF9WNA)

【配置密钥】

ssh -i 【密钥的路径】 -p 30480 ma-user@dev-modelarts.cn-southwest-2.huaweicloud.com

说明：-p指定的端口号，每个端口号对应一个notebook实例，目前我们实例部署在30480

配置后运行看看能不能连上

【配置remote-ssh】

![img](https://wcn9wp389ugs.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDAzMDZhOTM1NDNkODA3M2I5M2VjNjA5YmExZmE2ZWJfWFFEVnk3dVZXV3p1TzJQaE5pcGNoSDhPZFZJUG1ZbkdfVG9rZW46V2ZHbGI5SUZDb0xCOWJ4TDZTVmMxcXpxblJlXzE3NTE0NjQxNjA6MTc1MTQ2Nzc2MF9WNA)

![img](https://wcn9wp389ugs.feishu.cn/space/api/box/stream/download/asynccode/?code=ODE2YzFhYTBlNTdiYjZhYjJkNTNhZmM2ZGU3NzViMmRfNHdTSDFGOUFvRUZzdTFKOVFRa1liS2poeU5MN2RKZDFfVG9rZW46UmZJbGJEeU9sb1FhUFR4T3VmeGM1QVRiblZkXzE3NTE0NjQxNjA6MTc1MTQ2Nzc2MF9WNA)

![img](https://wcn9wp389ugs.feishu.cn/space/api/box/stream/download/asynccode/?code=ZmQ2YTRjMWNkYzBkYmEwMWNhNDg0ODAwY2E2M2RmNTJfTVVGNGFUcjRFanhmRkVITzBBSE1JYjFQZTlKaUViSEVfVG9rZW46T3M2V2Jla1ZPb1V6b0l4RVd6SWNQSVZXbnVkXzE3NTE0NjQxNjA6MTc1MTQ2Nzc2MF9WNA)

![img](https://wcn9wp389ugs.feishu.cn/space/api/box/stream/download/asynccode/?code=MWExNTdhNTA4OWEwNWU0NjgxMTA0MTUyODc0YzdhZDdfMnM0ME02WnprNTFNbGNxb2RrNVZ2VlRRMVJSUUd2MDNfVG9rZW46UHJZMGJqZ3Z2b0lEZGx4dFhIbmNkZ2x4bk5lXzE3NTE0NjQxNjA6MTc1MTQ2Nzc2MF9WNA)

在方框中输入ssh -i 【密钥的路径】 -p 30480 ma-user@dev-modelarts.cn-southwest-2.huaweicloud.com

![img](https://wcn9wp389ugs.feishu.cn/space/api/box/stream/download/asynccode/?code=ZTM0YzMyM2EwMWE1OWM4YzcwYTRiODg2OTcyZjAyMmJfVjFRbVVtbXRoMXBLQnBvR3M1VVl1OUxGcUl6MVRZY05fVG9rZW46WDRjR2JwQ2lubzVaOGl4elJMdmNBZHNMbmhnXzE3NTE0NjQxNjA6MTc1MTQ2Nzc2MF9WNA)

选linux，就ok了