可以，你就把“当前要做计划”改成下面这个版本，既能执行，也方便你打勾记录。

````text
# 当前任务：搞清楚“原始数据很多，但训练集只有几百个 clip”

## 0. 进度 Checklist

[ ] 检查目录结构  
[ ] 检查数据文件类型  
[ ] 检查训练 manifest / train list  
[ ] 检查环境工具：python / pandas / ffprobe  
[ ] 检查当前项目配置：数据路径、训练参数、dataset config  
[ ] 写 metadata 统计脚本  
[ ] 跑 fullsubset metadata 统计  
[ ] 跑候选 complete clips 筛选  
[ ] 对比训练 manifest 与原始 clip  
[ ] 写最终记录：结论 + 不确定字段 + 下一步  

---

## 1. 检查目录结构

目标：确认 `/mnt/data/csgo-datasets-fullsubset` 是什么层级。

命令：

```bash
find /mnt/data/csgo-datasets-fullsubset -maxdepth 3 -type d | head -n 100

find /mnt/data/csgo-datasets-fullsubset -mindepth 2 -maxdepth 2 -type d | wc -l

find /mnt/data/csgo-datasets-fullsubset -mindepth 3 -maxdepth 3 -type d -name train | wc -l

find /mnt/data/csgo-datasets-fullsubset -mindepth 3 -maxdepth 3 -type d -name meshes | wc -l
````

记录：

```text
fullsubset 目录结构：

/mnt/data/csgo-datasets-fullsubset
└── level1_hash:
    └── level2_hash:
        ├── train
        └── meshes

level2_hash 数量：
train 目录数量：
meshes 目录数量：

初步判断：
```

---

## 2. 检查数据文件类型

目标：确认 `train/` 里是否包含 RGB、depth、seg、motion、player state、visibility。

命令：

```bash
find /mnt/data/csgo-datasets-fullsubset -path "*/train/*" -type f | head -n 100
```

统计模态：

```bash
find /mnt/data/csgo-datasets-fullsubset -path "*/train/*" -type f \
| grep -E "\.mp4$|_depth\.mkv$|_seg\.mkv$|_motion\.bin$|_player_visibility\.json$|\.json$" \
| sed -E 's/.*(_depth\.mkv|_seg\.mkv|_motion\.bin|_player_visibility\.json|\.mp4|\.json)$/\1/' \
| sort | uniq -c | sort -nr
```

记录：

```text
.mp4 数量：
_depth.mkv 数量：
_seg.mkv 数量：
_motion.bin 数量：
普通 .json 数量：
_player_visibility.json 数量：

是否看起来是一组 basename 对应多个模态文件：
[ ] 是
[ ] 否
[ ] 不确定
```

---

## 3. 检查训练 manifest / train list

目标：找到当前模型训练实际用了哪些 clip。

命令，在项目根目录跑：

```bash
find . -maxdepth 5 -type f | grep -Ei "manifest|train|val|test|split|list|dataset|jsonl|csv|txt"
```

如果候选太多，再看文件大小和前几行：

```bash
wc -l path/to/candidate_file
head -n 5 path/to/candidate_file
```

如果是 JSON：

```bash
python -m json.tool path/to/candidate_file | head -n 80
```

记录：

```text
找到的候选 manifest：

1.
路径：
行数 / 条数：
entry 长什么样：
是否包含 clip path / basename：
是否包含 map/player/duration：
判断：可能是 / 不是训练 manifest

2.
路径：
行数 / 条数：
entry 长什么样：
是否包含 clip path / basename：
是否包含 map/player/duration：
判断：可能是 / 不是训练 manifest

当前训练集估计 clip 数：
train：
val：
test：
total：
```

---

## 4. 检查环境工具

目标：确认能否跑统计脚本。

命令：

```bash
which python
python --version

python - <<'PY'
try:
    import pandas as pd
    print("pandas OK", pd.__version__)
except Exception as e:
    print("pandas not available:", e)
PY

which ffprobe || true
ffprobe -version | head -n 1 || true
```

记录：

```text
python 路径：
python 版本：
pandas：
ffprobe：
是否可以先跑无 ffprobe 版本：
[ ] 可以
[ ] 不可以
```

---

## 5. 检查当前项目配置

目标：找训练代码/配置里到底用哪个数据路径、哪个 manifest。

命令：

```bash
find . -maxdepth 4 -type f | grep -Ei "config|yaml|yml|toml|json|py|sh" | head -n 200
```

重点搜索数据路径：

```bash
grep -R "/mnt/data/csgo" -n . | head -n 50
grep -R "csgo-datasets" -n . | head -n 50
grep -R "manifest\|train_list\|dataset" -n . | head -n 100
```

记录：

```text
配置文件路径：

数据 root 设置为：

manifest / split 设置为：

训练脚本入口可能是：

dataset 类 / dataloader 可能是：

不确定点：
```

---

## 6. 写 metadata 统计脚本

目标：创建：

```text
tools/scan_csgo_metadata.py
```

要求支持：

```text
.mp4
_depth.mkv
_seg.mkv
_motion.bin
普通 .json
_player_visibility.json
navmesh.json / static_props.json / meshes
```

输出：

```text
outputs/fullsubset_metadata.csv
outputs/fullsubset_summary.json
outputs/candidate_complete_clips.csv
```

记录：

```text
脚本路径：
是否成功运行：
[ ] 是
[ ] 否

遇到的问题：
```

---

## 7. 跑 fullsubset 数据统计

命令：

```bash
python tools/scan_csgo_metadata.py \
  --roots /mnt/data/csgo-datasets-fullsubset \
  --out_csv outputs/fullsubset_metadata.csv \
  --out_json outputs/fullsubset_summary.json
```

查看结果：

```bash
cat outputs/fullsubset_summary.json
head -n 5 outputs/fullsubset_metadata.csv
```

记录：

```text
总 basename group 数：
完整多模态 clip 数：
level1_hash 数：
level2_hash 数：
episode 数：
player 数：

缺 RGB 数：
缺 depth 数：
缺 seg 数：
缺 motion 数：
缺 player_state 数：
缺 visibility 数：
```

---

## 8. 粗筛候选 complete clips

筛选标准：

```text
has_rgb == True
has_depth == True
has_seg == True
has_motion == True
has_player_state == True
has_player_visibility == True
文件大小 > 0
```

记录：

```text
candidate_complete_clips.csv 路径：

候选完整 clip 数：

前 10 个候选 clip 示例：
1.
2.
3.
```

---

## 9. 对比训练 manifest 和原始数据

目标：解释为什么原始数据很多但训练只有几百个 clip。

记录：

```text
训练 manifest clip 数：
fullsubset 原始完整 clip 数：
训练 clip / 原始完整 clip 比例：

是否发现训练只用了某些 level1_hash：
[ ] 是
[ ] 否
[ ] 不确定

是否发现训练只用了某些 level2_hash：
[ ] 是
[ ] 否
[ ] 不确定

是否发现训练只用了某些 player：
[ ] 是
[ ] 否
[ ] 不确定
```

---

## 10. 最终结论记录

```text
目前结论：

1. 数据目录结构是：


2. 一个 clip group 大概由这些文件组成：


3. 当前训练 manifest 位置是：


4. 当前训练实际使用 clip 数是：


5. 原始 fullsubset 里完整 clip 数是：


6. “原始数据很多但训练集只有几百个 clip”的可能原因：


7. 已生成文件：
- 
- 
- 

8. 还需要问学长确认的问题：
- clip 的准确定义是否等于 basename group？
- level1_hash / level2_hash 分别代表什么？
- train 文件夹是否等于最终训练 split？
- duration 应该从 mp4 还是 motion/json 里读？
- fullsubset 和 csgo-datasets 是否有重复？
```

```

你可以把这个直接放进你的 `notes.md` 或任务记录里。这样你每跑完一步就打一个 `[x]`，不会再出现“跑了很多命令但不知道自己推进到哪了”的感觉。
```