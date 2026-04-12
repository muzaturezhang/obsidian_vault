
## topic1

### Problem/Task/Objective：假谣言未来热度预测

输入：已有谣言（同时包括发布谣言者的资料）    -> 输出： 未来热度值（【这个量化指标该如何来定？】）

### Limitation/Gap：跨事件泛化能力不足，跨事件/跨时间模型迁移时模型的稳定性不够（模型可能会失效）

### Contribution
1. 可解释性:相关性解释 -> **反事实解释** （解释causal、语言现象）(在不同事件域上验证)
2. 因果去偏：利用 **对抗域适应（Adversarial）** 或 **IRM风格的风险不变约束** ，将 **事件/主题** 这些confounders（混杂变量/干扰因素）作为环境，使其 **保持不变**
> 在预测时，模型容易根据 **事件/主题** 这样的 **shortcut** 来预测热度，而并非从 **内容** 本身出发，因此可以将它们作为 **环境**

3. 新评测协议：利用 ** OOD (Out of distribution) ** 与 ** Early Trancation ** 的办法提高模型的跨事件泛化能力，更接近实际的预测场景
> 事件OOD：eg. 在【金融/娱乐】主题的数据上train，在【疫情】主题的数据上test
> 时间OOD：eg. 在2022年的数据上train，在2024年的数据上test
> 早期截断：利用谣言发布后短时间内的少量信息进行预测 （【是否可以建立一个 **信息发布后早期数据** 的数据集作为创新点】）


### Existed Work
- Develop a neural model
	> 可结合【Computational Linguistics】学科的知识设计 **handcrafting features** ，既可以作为预测模型的判断因素，也可以通过预测模型来筛选更关键的 **features** 反向为【计算语言学】作出研究贡献

### Interdisciplinary Knowledge

- Computational Linguistics
	- temporal concept drift（数据的规律会随着时间变化）





