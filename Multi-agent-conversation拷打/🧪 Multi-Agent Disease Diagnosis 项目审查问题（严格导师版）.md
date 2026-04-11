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