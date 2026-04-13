## 🧩 Prompt 1：标准结构框架总结（最推荐）

```text
You are a research-level instructor.

Given the following material (paper / code / article), produce a structured overview that helps me build a clear mental model.

Your output must include:

1. High-level structure
   - Break the material into major components / sections
   - Give each part a clear name

2. Relationships between components
   - Explain how the parts connect
   - What depends on what
   - What is the flow of logic

3. Core problem and core idea
   - What problem is being solved?
   - What is the key idea or insight?

4. Key concepts and intuition
   - Identify the most important concepts
   - Explain them in simple but precise terms

5. Mechanism overview (important)
   - Describe how the method/system works step by step
   - Do not go into low-level detail yet

Avoid:
- Copying sentences
- Listing without explanation
- Superficial summaries

Focus on clarity, structure, and insight.

Material:
[PASTE HERE]
```

---

# 🧩 Prompt 2：更“硬核”的版本（适合论文/代码）

👉 如果你想更接近“研究级理解”

```text
Act as a PhD advisor.

Summarize the following material by constructing a structured mental model.

Your response must include:

1. Structural decomposition
   - What are the main modules/components?
   - Why is each part necessary?

2. Logical flow
   - How does the method progress from input to output?
   - What is the pipeline?

3. Core insight
   - What is the key idea that makes this work?
   - Why does it work (intuitively)?

4. Key abstractions
   - What are the central concepts or variables?
   - What role does each play?

5. Minimal working understanding
   - If I had to re-implement or explain this, what are the essential steps?

6. Common confusion points
   - What parts are most likely to be misunderstood?

Be concise but deep. Avoid generic explanations.

Material:
[PASTE HERE]
```

---

# 🧩 Prompt 3：代码专用（非常重要）

👉 针对 GitHub / Python code

```text
You are a senior engineer and ML researcher.

Analyze the following code and produce a structured explanation.

Include:

1. Overall purpose
   - What does this code do?

2. Module structure
   - Key functions/classes and their roles

3. Execution flow
   - Step-by-step what happens when the code runs

4. Data flow
   - What data is passed between components?

5. Key logic
   - The most important operations or algorithms

6. Abstractions
   - What are the core variables and what do they represent?

7. Simplified mental model
   - Explain the system in a way that can be remembered

Avoid line-by-line explanation unless necessary.

Code:
[PASTE HERE]
```

---

# 🧩 Prompt 4：超强版本（生成“认知地图”）

👉 如果你想更高级一点

```text
You are an expert in knowledge structuring.

Transform the following material into a clear mental map.

Your output should:

- Organize the content into a hierarchy (like a tree)
- Show relationships (cause-effect, dependency, flow)
- Highlight the core idea
- Identify the key concepts and how they interact

Then:
- Provide a short "one-paragraph summary" of the entire system
- Provide a "3-sentence essence" version

Material:
[PASTE HERE]
```

---

# 🔥 Bonus：配合你的“问题学习法”

你可以再加一句：

```text
After the structure summary, generate 5–8 macro-level questions to test understanding of this structure.
```

👉 这样直接进入你的 question system

---

# 🚨 一个关键提醒（非常重要）

👉 不要让 AI 一步做完所有事情

推荐流程：

---

## Step 1

👉 用这个 prompt → 拿结构

---

## Step 2

👉 用你之前的 prompt → 拿问题

---

## Step 3（关键）

👉 自己复述结构（不看答案）

---

👉 这一步才是真正 learning

---

# 🧭 最后一句总结

👉  
**好的结构 prompt 的核心不是“总结内容”，而是“强制 AI 显式化隐含结构（modules + relations + flow + core idea）”**

---

# 🚀 如果你想再升级（强烈推荐）

我可以帮你做一个更狠的东西：

👉  
**“针对一篇论文（比如 DINO），生成完整结构 + 问题树 + 学习路径”**

这个会直接把你带到“能读 paper + 能套瓷”的水平。