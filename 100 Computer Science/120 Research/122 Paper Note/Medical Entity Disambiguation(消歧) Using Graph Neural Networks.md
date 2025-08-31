---
Date: 2025-08-27
tags:
  - CS
  - graphRAG
  - research
  - GNN
---

[Medical Entity Disambiguation Using Graph Neural Networks](https://arxiv.org/pdf/2104.01488)


## 研究背景

Medical knowledge bases (KBs) 包括 **clinical resources(临床资源), electronic health records(电子健康记录）, and laboratory tests(实验室测试)** 的数据. 
但是，这些 data 中的 entity可能不是**canonical descriptions**in the KB.
e.g., using abbreviations, synonyms, or misspellings.


------------------------------------------------------------------------

## ED-GNN Method

- **end-to-end** framework (端到端)
- tackle the entity disambiguation problem in medical text
- based on three representative GNN models: **GraphSAGE, R-GCN, and MAGNN**
- 结合**contextual information** and **structural dependencies**

### ED-GNN 流程

>**construc a query graph**
	Nodes represent **候选实体** for each mention in the text.
	Edges encode **relationships** among these candidates.

>**利用GNN process the graph**
>    聚合邻居节点信息进行信息传播，使 学到的embeddings同时具有**contextual and structural cues**.

> 用 **classifier** predicts the correct entity based on **learned embeddings**


------------------------------------------------------------------------

## 实验结果

ED-GNN achieves an average F1 score improvement of 7.3% over state-of-the-art baselines across five real-world datasets.