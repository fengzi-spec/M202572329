# M202572329

prompt for learning by questioning

**提示词 baseline**:

    请从实际应用落地的可行性、核心工作的代价和收益矛盾、实验场景和负载的代表性这几个方面，对这项工作提出质疑

**常用模型**：DeepSeek、KIMI、豆包、文心、ChatGPT

**交叉评价**:

$$\{evaluator(reviewer(paper)) | reviewer, evaluator \in [DS, KM, DB], paper \in ReadingList\}$$

0. 基于**学术评价参考论文**，准备评分提示词 $Prompt_{evaluator_{id}}$
1. 在 reviewer 模型中，上传目标论文，使用提示词 $Prompt_{baseline}$ 质疑论文，得出**向论文的提问** $Question_{paper}$
2. 在 evaluator 模型中，上传目标论文，使用评分提示词，对 $Question_{paper}$ 打分
3. 根据 reviewer 和 evaluator 所用模型，归纳数据

**学术评价参考论文**

1. **IEEE Network Reviewer Guidelines**  
   **来源**: IEEE Communications Society  
   **链接**: [IEEE Network 审稿指南](https://www.comsoc.org/publications/magazines/ieee-network/reviewer-guidelines)  
   **说明**: 强调对方法理论完备性和实验可重复性的评估标准。
2. **Wang, Y., Zhang, L., & Chen, H. (2017)**  
   *Questioning Techniques Promote Critical Thinking in Engineering Education*  
   **期刊**: IEEE Transactions on Education  
   **链接**: [IEEE Xplore](http://ieeexplore.ieee.org/document/7942978/)  
   **说明**: 该研究验证了创新性质疑对工程教育中论文修改后创新指数提升23%的量化效果。
3. **Gupta, R. et al. (2021)**  
   *Models for Finding Quality Questions in Scientific Discussions*  
   **会议**: ACL  
   **链接**: [ACL Anthology](https://aclanthology.org/2021.acl-long.32/)  
   **说明**: 基于BERT的语义相似度计算框架（F1=66.6%）。
4. **Shin, H. et al. (2025)**  
   *Mind the Blind Spots: A Focus-Level Evaluation Framework for LLM Reviews*  
   **预印本**: arXiv:2502.17086  
   **链接**: [arXiv](https://arxiv.org/abs/2502.17086)  
   **说明**: 量化分析LLM生成的评审对技术有效性关注度比人类高30%，但创新性评估不足。
5. 严炜炜,黄为,温馨. 学术社交网络问答质量智能评价与服务优化研究[J]. 图书情报工作,2021,65(6):129-137.
6. 吴雅威,张向先,陶兴,等. 基于用户感知的学术问答社区答案质量评价指标构建[J]. 情报科学,2020,38(10):141-147

**准备评分提示词**

    现在希望能够给学术研讨小组找到一个系统性的方法，应用大语言模型推理来帮助提升同学们论文研讨的质量，结合目标论文，通过开发特定提示词，引导、鼓励同学们进行相关研究工作基础知识的追溯、有思想深度的质疑，以及研究合理性的批判。请结合这篇论文，考虑高质量质疑和研讨的关键要素，综合进行科学评分，构造一套对"提问质量"进行评分的提示词，提示词的使用方法是结合一篇论文及对这篇论文的提问，对所提问题进行0到10分的评价。

**评价流程**

    本次评价中，选择了论文Questioning Techniques Promote Critical Thinking in Engineering Education作为评价参考，然后5个ai模型对论文进行评价，这里展示质疑情况的总结如下所示：
    （1.qwen）IMPRESS 的核心思想——基于重要性剪枝 + 多级存储优化 I/O——具有启发性，尤其对高共享、长上下文、SSD 瓶颈场景可能有效。然而，其部署复杂度、假设依赖性、负载通用性等方面存在明显挑战。在缺乏真实业务 trace 验证、未与工业级推理引擎集成、且未覆盖边缘 case 的前提下，其“2.8× TTFT 降低”的收益可能难以复现于实际系统。建议未来工作：发布 trace 驱动的开源 benchmark，与 vLLM/TGI 集成，在真实客服/知识库场景中 A/B 测试。 
    （2.deepseek）IMPRESS 在减少TTFT方面展示了潜力，但其实际落地需解决硬件兼容性、动态适应性和工程集成问题。核心优化带来的收益可能被额外开销和复杂性部分抵消，且实验场景未能充分覆盖真实世界的复杂负载。未来工作需要在更广泛的生产环境中验证其鲁棒性，并探索自适应参数调整机制以平衡代价与收益。
    （3.kimi）
| 维度        | 质疑点                                |
| --------- | ---------------------------------- |
| **落地可行性** | 假设依赖模型结构，通用性差；系统复杂度高，稳定性难保证        |
| **代价与收益** | I/O 节省代价是计算/管理开销，权衡不清；精度评估场景过于温和   |
| **实验代表性** | 数据集构造人为制造重复前缀；模型与硬件配置偏理想，未考虑真实服务环境 |
    （4.文心一言）
    

## 评分统计

对论文 FLATQUANT: Flatness Matters for LLM Quantization 进行DeepSeek、KIMI、豆包、文心的质疑与相互评分统计，共得到16组得分。

| 质疑模型 | Deepseek打分 | Kimi打分 | 豆包打分 | 文心打分 |
|:-----------------:|:---------:|:-----:|:-----:|:---------:|
| Deepseek         | 7.8      | 8.6  | 8.2  | 8.4      |
| Kimi             | 8.6      | 8.8  | 8.6  | 8.8      |
| 豆包             | 8.4      | 8.4  | 8.8  | 8.6      |
| 文心一言         | 7.8      | 8.0  | 8.4  | 8.2      |

