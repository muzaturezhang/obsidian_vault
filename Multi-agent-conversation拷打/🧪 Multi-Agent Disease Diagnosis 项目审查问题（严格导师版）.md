---
Date: 2026-04-11
---

好的，下面是整理后的 **Markdown 版本（可直接粘到 Obsidian / README / Notion）**，结构已经帮你优化成更像**科研 review checklist + 导师拷问清单**👇

---

# 一、方法本质理解（Understanding Your Method）

## 1. 方法的核心贡献是什么？

- 你的 multi-agent 方法相较已有工作**新在哪里**？
    
- 是：
    
    - 提出了新的机制？
        
    - 还是已有框架（如 AutoGen）的应用？
        
- 如果只是：
    
    - 改 agent 数量 / prompt  
        👉 这属于 engineering 还是 research？
        

---

## 2. 为什么 Multi-Agent 有效？

- 为什么多个 agent 能 outperform 单个 LLM？
    
- 机制解释是什么：
    
    - diversity？
        
    - self-correction？
        
    - majority voting？
        
    - 更长 context？
        

👉 关键追问：

- 为什么不用：
    
    - self-consistency？
        
    - ensemble？
        

👉 如何证明：

> 性能提升来自 multi-agent interaction，而不是多次采样？

---

## 3. Agent 角色设计是否必要？

- doctor agent 和 supervisor agent 的区别是什么？
    
- supervisor 的作用：
    
    - 控制流程？
        
    - 聚合结果？
        
    - 提供 reasoning？
        

👉 如果：

- 去掉 supervisor
    
- 用 majority voting
    

👉 性能会下降吗？为什么？

---

## 4. 是否真正实现了“多 agent 交互”？

- agent 之间是否存在：
    
    - 信息更新（state update）？
        
    - belief revision？
        
    - disagreement resolution？
        

👉 还是只是：

- 顺序发言 + 重复观点？
    

👉 如果是后者：

> 本质上只是 chain-of-thought 变体

---

# ⚙️ 二、设计合理性（Design Justification）

## 5. 为什么不用这些 baseline？

必须回答：

- 单模型 + CoT
    
- Self-consistency
    
- Self-refine（iterative refinement）
    

👉 如果没有这些对比：

> ❗实验不成立

---

## 6. LLM 是否真的模拟“不同医生”？

- 不同 agent 是否具有：
    
    - 不同 reasoning 风格？
        
    - 不同知识偏好？
        

👉 如何验证：

- diversity 是否存在？
    

👉 如果没有：

> 本质是同一个模型自言自语

---

## 7. 为什么选择 rare disease？

- rare disease 的特点：
    
    - 数据稀缺
        
    - 高不确定性
        

👉 问题：

- 方法是否只在 rare disease 有效？
    
- 在 common disease 上是否成立？
    
- 是否做 cross-domain evaluation？
    

---

# 🧪 三、实验严谨性（Experimental Rigor）

## 8. Evaluation metric 是否合理？

- 使用：
    
    - top-1 accuracy？
        
    - top-k？
        
    - differential diagnosis？
        

👉 医学任务问题：

- 一个 case 可能多个合理答案
    

👉 如何处理：

- partial correctness？
    

---

## 9. 数据规模是否足够？

- 当前：302 cases
    

👉 问题：

- 是否有 statistical significance？
    
- 是否计算：
    
    - variance？
        
    - confidence interval？
        

👉 如果换数据：

> 结果是否稳定？

---

## 10. 是否控制随机性？

- 是否：
    
    - 固定 seed？
        
    - 多次运行取平均？
        

👉 如果没有：

> ❗结果可能是偶然

---

## 11. 是否存在 data leakage？

- 数据是否可能出现在 LLM 训练集中？
    

👉 如果是：

> 实验可能测的是 memorization

---

## 12. 是否做了 Ablation Study？

必须包含：

- agent 数量 vs performance
    
- 有无 supervisor
    
- 对话轮数
    

👉 如果没有：

> ❗无法解释方法有效性

---

# 📊 四、结果解释（Result Interpretation）

## 13. 性能提升来源是什么？

- 提升是否来自：
    
    - multi-agent interaction？
        
    - 还是更多 token / compute？
        

👉 对比：

- 单模型 + 更长推理
    

👉 是否还能达到相同效果？

---

## 14. Failure Cases 分析

请列出：

- multi-agent 失败案例
    
- disagreement 无法解决的情况
    
- hallucination 放大的情况
    

👉 如果没有：

> ❗对方法理解不足

---

## 15. 是否存在“错误放大”问题？

- 如果第一个 agent 错：
    
    - 后续 agent 是否：
        
        - reinforce bias？
            
        - groupthink？
            

👉 是否有实际案例？

---

# 🧠 五、隐含假设（Hidden Assumptions）

## 16. 核心假设是什么？

请明确：

- LLM 可通过讨论改进推理
    
- agent 能产生有效分歧
    
- 多轮对话不会 drift
    

👉 如果不成立：

> 方法是否崩溃？

---

## 17. 方法是否 scalable？

- agent 数量增加会：
    
    - 提升 performance？
        
    - 增加 cost？
        
    - 引入不稳定性？
        

👉 是否存在：

> diminishing returns？

---

# 🔥 六、致命问题（Reviewer-Level Attacks）

## 18. Reviewer 质疑

如何回应：

> “Multi-agent is unnecessary. Similar gains can be achieved with self-consistency.”

👉 你的 rebuttal 是什么？

---

## 19. 与已有工作的关系

- 在什么 setting 下更强？
    
- 在什么 setting 下更弱？
    

👉 是否做过：

- 系统性对比？
    

---

## 20. 最关键问题

如果替换为：

> GPT-4 + 多次 self-consistency + voting

👉 你的方法是否仍然更好？

👉 如果不能确定：

> ❗方法可能没有核心贡献

---

# 🧭 导师总结（Critical Verdict）

## 当前最大问题：

> ❗尚未证明 multi-agent interaction 的必要性

---

## 下一步必须做：

- 构建强 baseline（self-consistency / CoT / refine）
    
- 做完整 ablation study
    
- 分析 failure cases
    
- 明确机制解释（不是现象描述）
    

---

如果你下一步想冲**顶会级别**，我可以帮你做一件更关键的事：

👉 把这份 checklist **转成一套完整实验设计（直接写论文那种）**


---

<br>
<br>
下面是**机制层（mechanism-level）拷问问题**，我会用**严格 PhD 导师视角**来问——重点不是“你做了什么”，而是**系统到底是怎么工作的，以及为什么这么设计**。

---

# 🧠 Multi-Agent Diagnosis（机制层深度拷问）

---

## 1. 系统信息流（必须逐步解释）

👉 **Step-by-step 问题**

请你从输入到输出，逐步解释整个系统：

- 输入一个病例后：
    
    1. 第一个 agent 收到的 prompt 是什么？
        
    2. 它的输出结构是什么（diagnosis / reasoning / confidence？）
        
    3. 第二个 agent 接收到了哪些信息？是原始 case 还是前一个 agent 的输出？
        
    4. supervisor 在哪一步介入？
        
    5. 最终 prediction 是如何产生的？
        

👉 要求你：

> 用“数据流”的角度，而不是“代码流程”

---

## 2. Multi-agent interaction 的本质机制

👉 **Why 问题**

- 你的系统中，agent 之间的信息交互本质上是：
    
    - conditioning？
        
    - iterative refinement？
        
    - belief update？
        

👉 为什么这种交互方式能够改善推理？

👉 如果只是：

> y₂ = f(x, y₁)

👉 那你如何证明这不是：

> 更深一层的单模型推理？

---

## 3. Agent diversity 是如何产生的？

👉 **Why 问题**

- 所有 agent 使用同一个 LLM 吗？
    
- 如果是：
    
    - diversity 从哪里来？
        
        - prompt？
            
        - temperature？
            
        - role description？
            

👉 如果没有显式 diversity：

> 多 agent ≈ 多次相同采样

👉 那为什么你认为：

> 它比 self-consistency 更强？

---

## 4. Supervisor 的机制作用

👉 **Why 问题**

- supervisor 是如何改变系统状态的？
    

👉 它是：

- 只做 final aggregation？
    
- 还是会 influence 中间 reasoning？
    

👉 如果 supervisor 的作用是：

> select / summarize

👉 那它和：

- voting
    
- reranking
    

👉 本质区别是什么？

---

## 5. 推理链是如何被“修改”的？

👉 **Step-by-step 问题**

假设：

- agent A 给出错误 diagnosis
    
- agent B 看到 A 的输出
    

👉 请你逐步解释：

1. B 如何检测 A 的错误？
    
2. B 是否有能力：
    
    - reject？
        
    - revise？
        
3. 如果 B 不同意 A：
    
    - 系统如何处理冲突？
        

👉 如果没有显式机制：

> 那 disagreement 是如何被利用的？

---

## 6. 系统的隐式目标函数是什么？

👉 **核心机制问题**

你的系统没有显式 loss function，但实际上在优化某个目标：

👉 请回答：

- 这个系统在优化什么？
    
    - accuracy？
        
    - consistency？
        
    - likelihood？
        

👉 如果写成形式化：

> y = argmax_y P(y | x, interaction)

👉 那么：

- interaction 在这个概率中扮演什么角色？
    

---

## 7. 为什么需要多轮对话？

👉 **Why 问题**

- 多轮 interaction 的收益是什么？
    

👉 请解释：

- 第 t 轮 vs 第 t+1 轮：
    
    - 信息发生了什么变化？
        
    - entropy 是否降低？
        

👉 如果：

- 性能在 2 轮后不再提升
    

👉 是否说明：

> interaction 已经 saturate？

---

## 8. 信息是如何累积还是污染的？

👉 **机制风险问题**

- 每一轮对话都会把之前的内容加入 context
    

👉 问题：

- 这是：
    
    - information accumulation？
        
    - 还是 noise accumulation？
        

👉 如何判断：

- 后面的 agent 是在利用信息  
    还是被误导？
    

---

## 9. 你的系统是否等价于某种已知方法？

👉 **结构等价问题**

请你判断：

你的系统是否等价于以下之一？

- iterative refinement
    
- self-consistency + conditioning
    
- tree-of-thought（ToT）
    

👉 如果等价：

> 那你的贡献是什么？

👉 如果不等价：

> 请明确指出“关键差异机制”

---

## 10. 错误传播机制（failure propagation）

👉 **Step-by-step 问题**

假设：

- 第一个 agent hallucinate 了一个症状
    

👉 请逐步分析：

1. 这个错误如何进入后续 context？
    
2. 后续 agent 是否会：
    
    - 质疑？
        
    - 接受？
        
3. 最终 prediction 是否会被污染？
    

👉 如果系统没有：

- error correction mechanism
    

👉 那 multi-agent 是否可能：

> 放大错误？

---

## 11. 你的系统是否真的在“推理”？

👉 **本质拷问**

- 你的系统是：
    
    - reasoning system？
        
    - 还是 language pattern generator？
        

👉 关键问题：

- agent 的“讨论”是否改变了：
    
    - latent representation？
        
    - 还是只是生成更多文本？
        

👉 如果只是文本：

> 那 reasoning improvement 从何而来？

---

## 12. 极限情况分析（机制边界）

👉 **深度理解问题**

请分析：

### 情况 1：

- 所有 agent 完全一致  
    👉 系统会退化成什么？
    

### 情况 2：

- 所有 agent 完全随机  
    👉 系统会发生什么？
    

### 情况 3：

- agent 数量 → ∞  
    👉 是否会收敛？
    

👉 这些极端情况说明：

> 你的方法本质是什么？

---

# 🧭 导师点评（直说版）

如果你答不上这些问题，说明你目前停留在：

> ❗“我搭了一个系统”  
> 而不是  
> ✅“我理解了这个系统为什么有效”

---

如果你下一步想更狠一点训练自己，我可以帮你做：

👉 把这些问题变成  
**“面试 / 套瓷 / 答辩级别的回答模板（直接让你秒杀导师）”**