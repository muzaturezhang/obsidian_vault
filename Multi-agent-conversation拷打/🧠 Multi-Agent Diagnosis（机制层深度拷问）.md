下面是**机制层（mechanism-level）拷问问题**，我会用**严格 PhD 导师视角**来问——重点不是“你做了什么”，而是**系统到底是怎么工作的，以及为什么这么设计**。

---

# 

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