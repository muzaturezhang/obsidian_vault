V. A 
主要内容/侧重分析点：
1. 不同大小的模型(2.8B/1.4B/70M)对于member与non-member的熟悉程度是否有区别
（证明Min-K等MIA攻击方法的有效性合理性：只有有区别，才能通过Min-K等MIA方法来攻击）
2. 同时也印证了第四部分IV的结论：（1）quantization并不显著影响MIA的攻击效果，不destroy separability （2）model越大（eg. 2.8B>70M）MIA被影响的程度越小 （3）model越大，membership separability越大，对于member的memorization signal越高

V.B
主要内容/侧重分析点：重点分析哪些token type的member与non-member的gap最大（gap越大就说明对应的token type更容易泄漏、被MIA攻击，signal更强），得出结论

V. C
主要内容/侧重分析点/结论：1. Min-K具有Bias，不uniform（对于不同的token type selected ratio有很大差异）2. 具体分析不同token type的selected ratio，以及哪些更容易作为membership signal 3. 由于我们发现Fig5与Fig4并不完全一致，（比如fig4里common type并不是loss gap最大的，但它在fig5里却是占比最高的），说明Min-K不直接target high-gap token

V.D
主要内容/侧重分析点/结论：1. 印证上面，模型越小，quantization对于MIA效果的影响越大
2. 某些token type对于quantization的改变更sensitive，比如xxx