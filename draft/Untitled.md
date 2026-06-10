审查方 / 本地 Codex / 本地自动化脚本共用学长电脑上的 handoff 文件；真正跑实验的服务器 Codex 只通过 SSH 去服务器执行命令，然后把服务器结果路径写回本地 COMMS。

**如果要将整个读写体系移到服务器上是不是要改一下文件里的读写路径了**
**同时这意味着我的电脑要24小时开着吗** （不过到服务器上似乎就不会有这样的问题？（但是这样就没办法多个人用各自的号了？（想想怎么构建完善）））

***
方案 A：放你本地电脑
优点：配置简单，能直接读本地文件
缺点：电脑要开着，睡眠/断网就不跑

方案 B：放服务器
优点：24h 在线，更适合自动化
缺点：handoff / memory / claude 配置也要放服务器，权限和账号要配好

方案 C：本地手动跑
优点：最稳，适合你刚开始学
缺点：不自动
***

学长 Mac：
/Users/sunzhengqi/Desktop/科研项目/多视角/codex_handoff/
    README.md
    COMMS.md
    memory_codex.md
    training_codex.md

Codex 在学长 Mac 上运行
    ↓
读写本地 COMMS.md
    ↓
通过 ssh 登录服务器
    ↓
cd /mnt/workspace/zhengqi/multiview-map-v0
    ↓
跑实验 / 读结果 / 写 ledger
    ↓
把服务器路径和数字追加回本地 COMMS.md

这里有个问题，每次claude 醒来为什么不直接看codex那个md，还要再看一下长期记忆（还是说都要看，那长期记忆的用是什么呢）


如果现在的话

