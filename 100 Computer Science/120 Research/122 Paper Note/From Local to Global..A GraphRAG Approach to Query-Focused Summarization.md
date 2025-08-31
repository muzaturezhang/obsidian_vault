---
Date: 2025-08-12
tags:
  - research
  - graphRAG
  - CS
---
[From Local to Global: A GraphRAG Approach to Query-Focused Summarization](https://arxiv.org/pdf/2404.16130?)



## 研究背景与挑战

### 对比传统RAG

传统的 RAG 方法不善于处理**global questions directed at an entire text corpus**这种全局性问题

### 对比已有QFS方法

现有的 QFS 方法无法扩展到 typical RAG systems 索引的 **大量文本量级**



## GraphRag Method

>**构建实体知识图谱**
	derive an entity knowledge graph from the source documents.

>**生成社区摘要**
>	pregenerate **community summaries** for all groups of **closely-related** entities.

>**生成 response**
>	每个community summary 都总结 **partial response**
>	summarize partial responses into a **final response** to the user



## 实验结果


对于全局性问题 over datasets in the 1 million token range, Graph RAG 在 **comprehensiveness** and **diversity** 方面都较 传统RAG有显著性提升
