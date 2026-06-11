好，现在我们不要再发散。你接下来只做一件事：

# 把项目从“期中原型”补到“能展示的期末 pre 版本”

目标不是完美，而是：

> 后天 pre 时，你们有一个能跑的 demo、有截图、有对比实验、有 PPT 可讲。

我会按“手把手流程”带你走。你每完成一步，把结果/报错/截图发我，我再告诉你下一步。

---

# 总体路线

你现在要补齐的不是所有功能，而是这 4 个展示材料：

1. **能稳定运行的 main.py**
    
2. **输出文件：research_notes.txt / draft_report.txt / review.txt**
    
3. **截图：项目结构、核心代码、运行结果、review 输出**
    
4. **最小实验：Single LLM vs Multi-Agent 对比表**
    

今天先不要做 RAG、parallel scheduling。Web Search 和 Streamlit 等会儿再决定要不要加。

---

# Step 0：先确认你现在项目里到底有什么

你先在项目根目录运行：

```bash
pwd
find . -maxdepth 3 -type f | sort
find . -maxdepth 2 -type d | sort
```

你应该看到类似：

```text
./main.py
./agents/manager.py
./agents/researcher.py
./agents/writer.py
./agents/reviewer.py
./utils/llm.py
./outputs/...
```

你把这三条命令的输出发我。

---

# Step 1：确认 API key 和 DeepSeek 调用没问题

然后运行：

```bash
echo $DEEPSEEK_API_KEY
```

如果输出是空的，就重新设置：

```bash
export DEEPSEEK_API_KEY="你的key"
```

注意不要把 key 发给我。你只需要告诉我：

```text
echo 有输出 / echo 没输出
```

然后再检查 `utils/llm.py`，应该长这样：

```python
import os
from openai import OpenAI

client = OpenAI(
    api_key=os.getenv("DEEPSEEK_API_KEY"),
    base_url="https://api.deepseek.com"
)

def call_llm(role, prompt, model="deepseek-chat"):
    print(f"\n[{role}] running...")

    response = client.chat.completions.create(
        model=model,
        messages=[
            {"role": "user", "content": prompt}
        ]
    )

    return response.choices[0].message.content
```

你先确认这里有没有还是 `OPENAI_API_KEY` 或者 `responses.create`。如果有，改掉。

---

# Step 2：先跑通原系统

运行：

```bash
python main.py
```

你现在只需要看有没有出现：

```text
[Manager] Task received
[Research Agent] running...
[Writer Agent] running...
[Reviewer Agent] running...
```

如果成功，把终端输出截图保存成：

```text
runtime_output.png
```

如果报错，把完整报错发我。

---

# Step 3：确认输出文件有没有保存

你看一下有没有 `outputs/`：

```bash
ls -la outputs
```

如果没有，就在 `main.py` 里加：

```python
import os
os.makedirs("outputs", exist_ok=True)
```

然后在 `manager(topic, qos)` 后面保存：

```python
with open("outputs/research_notes.txt", "w", encoding="utf-8") as f:
    f.write(research_notes)

with open("outputs/draft_report.txt", "w", encoding="utf-8") as f:
    f.write(draft)

with open("outputs/review.txt", "w", encoding="utf-8") as f:
    f.write(review)
```

你的 `main.py` 最终大概应该是：

```python
import os
from agents.manager import manager

if __name__ == "__main__":
    os.makedirs("outputs", exist_ok=True)

    topic = "AI hardware development in 2024"
    qos = "lowest cost and fastest speed"

    research_notes, draft, review = manager(topic, qos)

    print("\n========== RESEARCH NOTES ==========")
    print(research_notes)

    print("\n========== DRAFT REPORT ==========")
    print(draft)

    print("\n========== REVIEW ==========")
    print(review)

    with open("outputs/research_notes.txt", "w", encoding="utf-8") as f:
        f.write(research_notes)

    with open("outputs/draft_report.txt", "w", encoding="utf-8") as f:
        f.write(draft)

    with open("outputs/review.txt", "w", encoding="utf-8") as f:
        f.write(review)
```

然后重新运行：

```bash
python main.py
ls -la outputs
```

这一步完成后，你要有 3 个文件：

```text
research_notes.txt
draft_report.txt
review.txt
```

---

# Step 4：准备 PPT 必备截图

你现在至少要截 4 张图：

## 图 1：项目结构

截图 VSCode 左边栏，能看到：

```text
agents/
utils/
outputs/
main.py
```

保存成：

```text
project_structure.png
```

## 图 2：Manager 代码

截 `agents/manager.py` 中这几行：

```python
research_notes = research_agent(topic, qos)
draft = writer_agent(topic, research_notes)
review = reviewer_agent(topic, draft)
```

保存成：

```text
manager_code.png
```

## 图 3：运行结果

截 terminal 中：

```text
[Manager] Task received
[Research Agent] running...
[Writer Agent] running...
[Reviewer Agent] running...
```

保存成：

```text
runtime_output.png
```

## 图 4：Reviewer 输出

打开：

```bash
cat outputs/review.txt
```

或者直接打开文件截图，保存成：

```text
reviewer_output.png
```

---

# Step 5：做最小实验，不要复杂

你需要补一个最小对比实验：

> Single LLM direct generation vs Multi-Agent workflow

先新建一个文件：

```bash
touch single_agent_baseline.py
```

内容写：

```python
import os
from utils.llm import call_llm

if __name__ == "__main__":
    os.makedirs("outputs", exist_ok=True)

    topic = "AI hardware development in 2024"

    prompt = f"""
Write a structured industry report about: {topic}.

Include:
1. Introduction
2. Key trends
3. Challenges
4. Conclusion
"""

    report = call_llm("Single LLM Baseline", prompt)

    print(report)

    with open("outputs/single_agent_report.txt", "w", encoding="utf-8") as f:
        f.write(report)
```

然后运行：

```bash
python single_agent_baseline.py
```

现在你会有：

```text
outputs/single_agent_report.txt
outputs/draft_report.txt
outputs/review.txt
```

---

# Step 6：做一个人工评分表

你不需要搞复杂自动评估。后天 pre 最小可用表格是这个：

|Method|Structure Completeness|Review Ability|Workflow Transparency|Comment|
|---|--:|--:|--:|---|
|Single LLM|3/5|No|Low|Directly generates one report|
|Multi-Agent System|5/5|Yes|High|Research → Writer → Reviewer|

你明天可以根据实际输出稍微改分数，但现在先放这个表到 PPT。

这张表就是你们的 preliminary evaluation。

---

# Step 7：如果还有时间，再加 Reflection Loop

这一步是加分项，不是必须。

你可以先完成上面 6 步。完成后我再带你加。

Reflection Loop 的效果是：

```text
Writer generates draft
↓
Reviewer gives feedback
↓
Writer revises draft based on feedback
```

这很适合 PPT 展示，但如果你现在系统还没稳定，先别动。

---

# 你现在先做哪一步？

现在立刻从 **Step 0** 开始。

运行：

```bash
pwd
find . -maxdepth 3 -type f | sort
find . -maxdepth 2 -type d | sort
```

把输出发我，我帮你判断当前项目结构有没有问题，然后继续下一步。