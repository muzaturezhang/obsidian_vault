---
Date: 2025-08-06
tags:
  - graphRAG
  - medical
  - CS
  - research
---
[Medical Graph RAG: Towards Safe Medical Large Language Model via Graph Retrieval-Augmented Generation](https://arxiv.org/pdf/2408.04187)


## 研究背景与挑战

### 对比普通LLM

LLM 在**医学领域**面临的挑战

>**知识容量有限**
>	医学领域基于vast knowledge databases，将繁杂的知识融入有限的上下文窗口几乎无法完成。
	
>**术语精确性无法保证**
>	医学有precise terminology system和大量的 established truth，LLM 生成的内容需确保术语准确性。
    
>**无法确定内容准确性**
>	LLM 可能会 distort, modify, or introduce creative elements into the data，没有准确的source.
    

### 对比传统RAG

>**难以合成新见解，将 retrieve 到的 knowledge 融入原response**

>**跨文档整体理解效果不好**


------------------------------------------------------------------------

## MedGraphRAG 

**MedGraphRAG创新点：

### Triple Graph Construction（三元图构建）

>**triple graph construction**
>    一种 triple-linked structure
   user documents - credible medical sources - controlled vocabularies(definition)

好处：
- enhance LLM reasoning
- 提高reliability and explainability(medical sources)

### U-Retrieval（统一检索）

预处理：
- 用 predefined medical tags 总结好每个 graph
- 对相似图迭代聚类
- 形成 multi-layer hierarchical tag structure, from broad to detailed tags.

>**Top-down Precise Retrieval**
>    过程：从大标签到小标签找到最相关的图，生成初步response
>    优点：提高 retrieval efficiency

>**Bottom-up Response Refinement**
>	过程；将大标签逐级重新整合回response中
>    优点：生成的response 有 global context awareness


------------------------------------------------------------------------

## MedGraphRAG整体工作流程

语义文档切分（Semantic Document Chunking）

实体抽取（Entities Extraction）
e = {name, type, context}







## 实验验证与结果

The results show that MedGraphRAG consistently outperforms state-of-the-art models across all benchmarks, while also ensuring that responses include **credible source documentation and definitions**.