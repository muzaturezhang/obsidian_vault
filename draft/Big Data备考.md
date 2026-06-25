
有，而且我觉得老师说的“计算和算法”大概率不是很复杂数学计算，而是这几类：公式代入、小表格手算、流程/算法步骤题。按你这 11 个 PPT 来看，真正需要重点准备的地方大概如下：

1. Data Mining 这一篇最可能出“计算/算法”  
    这是最核心的计算题来源。重点是 Association Rule Mining / Apriori。  
    可能考：  
    Support(X)=包含X的transaction数 / 总transaction数  
    Confidence(X=>Y)=同时包含X和Y的transaction数 / 包含X的transaction数  
    minsup / minconf 判断某个 itemset/rule 是否保留  
    Apriori principle：if an itemset is frequent, all of its subsets must also be frequent；if an itemset is infrequent, its supersets should not be generated/tested  
    Apriori algorithm：L1→C2→L2→C3→L3...，candidate generation + prune + scan DB count support  
    如果给一个购物篮表，让你找 frequent itemsets / association rules，这就是标准计算题。
    
2. Big Data Advertising 也可能出推荐算法计算  
    这里主要是 Recommendation Algorithms / Collaborative Filtering。  
    可能考：  
    Content-based filtering：根据 item features 推荐相似内容，概念题多。  
    Collaborative filtering：根据 user-item interactions 推荐。  
    User-Based CF：找 similar users，再根据 neighbors 推荐。  
    Item-Based CF：找 similar items，再预测用户对 item 的兴趣。  
    Cosine similarity：  
    sim(x,y)=rx·ry/(||rx||||ry||)  
    也可能给一个 user-item rating matrix，让你算两个用户/两个物品的 similarity，或者解释 raw utility matrix vs mean-centered utility matrix。这个比 Data Mining 的 Apriori 稍微次重点，但如果老师说有计算，CF 是很可疑的。
    
3. Hadoop / MapReduce 可能出“算法流程题”，不一定是数值计算  
    重点不是数学，而是让你写 MapReduce 如何处理 Word Count。  
    可能考：  
    Input files→split→map→intermediate key-value pairs→shuffle/group by key→reduce→output  
    Word Count 典型链路：  
    <line offset,line content>→map→<word,1>→shuffle/group→<word,[1,1,...]>→reduce→<word,count>  
    也可能问 Map 和 Reduce 各自做什么，shuffle/barrier 的作用是什么，JobTracker/TaskTracker 怎么调度任务。这个属于“算法/流程”题，不太像真正计算。
    
4. NoSQL 可能有轻量算法/判断题  
    重点可能是 CAP、consistent hashing、Dynamo/Cassandra。  
    可能考：  
    CAP：Consistency / Availability / Partition tolerance，三者不能同时完全满足；RDBMS≈CA，HBase/Bigtable≈CP，Cassandra/Dynamo≈AP。  
    Consistent hashing：key 映射到 hash ring，node 负责一段 hash range；节点增删时只影响局部数据迁移。  
    Dynamo N/R/W：N=replica number，R=read quorum，W=write quorum；如果讲到 quorum，常见判断是 R+W>N 更容易保证读到最新副本。不过如果 PPT 没展开，可能只是概念。  
    Cassandra write flow：client→coordinator→replicas→ACK；commit log→memtable→SSTable；hinted handoff/read repair。这个更像流程算法题。
    
5. Streaming Computing 可能考“处理模型算法”，但计算概率不高  
    可能考：  
    Spark RDD lineage：lost partitions can be reconstructed by lineage。  
    Narrow dependency vs wide dependency/shuffle。  
    Spark Streaming：input stream→DStream→RDD batches→micro-batch jobs。  
    Storm：Spout + Bolt + Topology。  
    Flink：stateful computation, exactly-once, event-time, checkpoint/savepoint。  
    这些更像“describe the processing model / compare systems”，不太像手算。
    
6. Cloud Storage / HDFS / GFS 可能考读写流程，不太可能考计算  
    可能考：  
    HDFS read：Client asks NameNode for block locations→reads directly from DataNodes。  
    HDFS write：Client→DN1→DN2→DN3 pipeline replication，ACK 反向返回。  
    GFS read/write：Master returns chunk handle + locations；client reads from chunkserver；write 中 Primary controls order and secondaries ACK。  
    Object storage vs block/file storage 对比。  
    这些是系统流程题，不是数值计算。
    
7. Cloud Infrastructure / Big Data Problems / Security / Industry Solution / Introduction 基本不太像计算题  
    这些主要是概念题、分类题、对比题：  
    Cloud models：IaaS/PaaS/SaaS，public/private/hybrid/community cloud。  
    Big Data problems：speed, type/structure, volume/flexibility, cost, value mining, security/privacy, sharing。  
    Security：cloud/big-data risk, privacy, data leakage, virtualization, multi-tenancy。  
    Industry solution：IBM/Oracle/Google/Open source systems and functionalities。  
    Introduction：Data Science definition, composition, descriptive/diagnostic/predictive/prescriptive analysis。  
    最多是“分类/匹配/describe”，不是算法计算。
    

所以你现在真正要准备的“计算/算法题优先级”应该是：  
最高优先级：Data Mining 的 Support / Confidence / Apriori。  
第二优先级：Advertising 的 Collaborative Filtering / Cosine Similarity / recommendation。  
第三优先级：MapReduce Word Count 流程。  
第四优先级：NoSQL consistent hashing / CAP / quorum / Cassandra write flow。  
第五优先级：Spark Streaming / Storm / Flink / RDD lineage 这种处理模型。

如果时间很紧，先把 Data Mining + Collaborative Filtering 的手算练一遍，因为这两个最像“考试计算题”。