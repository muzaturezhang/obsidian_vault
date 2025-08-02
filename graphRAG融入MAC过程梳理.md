---
Date: 2025-07-30
tags:
  - graphRAG
  - research
---
1. 传入一个医学数据集(里面有一堆病例)以及它要运用的大语言模型的配置文件
2. 利用命令行解析这个数据集文件，得出一个args对象(里面包含这个病例的相关信息以及使用的模型信息)
3. 利用args里的模型信息来初始化LLM模型

4. 用LLM模型逐个处理这个医学数据集中的每个病例
  > > 1. 给process_single_case这个函数传入LLM模型以及病例数据集的信息
  > > 2. 解析单个特定病例的信息为一些有关case的参数(一些case的标签)
  > > 3. 标明处理完单个case后生成文件的名称及其保存路径. (一些预处理)
  > 4. 生成处理这个case的所有医生智能体以及主管智能体、manager智能体，并加入agents列表中
  > 5. 设定多个agents在群聊中的发言轮数、次数等信息
  > 6. (现在的问题是怎样才能让这些agent都在发言的过程中调用graphRAG)


 5. 大语言LLM模型将输出的结果按照args里的路径生成文件；




neo4j graph_rag实现的功能：
	1. 生成一个graph_rag_pipeline
		(其中包含
			retriever(包含一个t2c的LLM`(先把text转化成cypher语言)`
				        一个driver`(驱动query相关信息)`   )
		     answer_llm(用于把检索到的信息生成最终答案)
	2. 生成一个query_knowledge_graph，用于传入、检索并返回

现在怎样把它融入MAC中呢：
直接 把MAC的每个agent每次生成answer这一个过程 替换为 调用一次query_knowledge_graph（但是好像不管什么时候调用query_knowledge_graph，最终用的实际上是同一个llm）

或者还有一种思路：
还是像原来一样在MAC_main.py中逐个生成agent，但是让这些agents在发言的时候每次都调用一下GraphRAG这个功能(但是不知道有没有这种功能)


排查一下报错原因：
1. 不加kg_expert时，可以跑通并生成会话文件
2. 单独人为输入问题并通过graphRAG返回答案，可以跑通
3. 使用其他agent生成问题，并通过graphRAG返回答案，不能跑通

>**整个过程使用的AI**
> 1. MAC中每个agent (✅)
> 2. GraphRAG中text2cypher的AI (✅)
> 3. GraphRAG中返回自然语言的AI (✅)


>**SSL 证书校验失败**
>1. 检查证书是否存在(✅)
>2. 