审查方 / 本地 Codex / 本地自动化脚本共用学长电脑上的 handoff 文件；真正跑实验的服务器 Codex 只通过 SSH 去服务器执行命令，然后把服务器结果路径写回本地 COMMS。

**如果这样的话岂不是要改一下文件里的读写路径了**

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