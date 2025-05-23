### 1. 预训练阶段
| 参数/指标 | 含义 | 必要性 |
|----------|------|--------|
| 模型架构 | 基础网络结构选择(Transformer、Llama等) | 决定模型基础能力上限和适用场景 |
| 参数规模 | 模型总参数量(如7B、13B) | 影响模型容量和训练资源需求 |
| 训练数据集 | 用于训练的语料库 | 决定模型的知识范围和语言能力 |
| 训练数据量 | 预训练数据的总量(TB或tokens) | 充分的数据量确保模型学习足够知识 |
| 批次大小 | 单次更新的样本数 | 影响训练稳定性和收敛速度 |
| 学习率 | 参数更新步长 | 过大过小都会影响训练效果 |
| 训练步数 | 总更新次数 | 确保模型充分学习数据中的模式 |
| 损失曲线 | 训练和验证损失变化图 | 监控训练进展和过拟合风险 |
| GPU资源 | 使用的计算设备数量和类型 | 影响训练速度和成本 |

### 2. 退火与学习率调整阶段
| 参数/指标 | 含义 | 必要性 |
|----------|------|--------|
| 退火策略 | 学习率调整方式(线性、余弦、阶梯式) | 帮助模型收敛到更好的局部最优 |
| 起始学习率 | 退火开始时的学习率 | 确保从合适的起点开始调整 |
| 结束学习率 | 退火结束时的学习率 | 防止过度调整导致无法学习 |
| 退火步数 | 完成退火过程的步数 | 控制退火速度，过快过慢都不利于训练 |
| 预热比例 | 学习率从0逐渐增加的阶段 | 避免训练初期的不稳定性 |
| 退火可视化 | 学习率变化曲线 | 直观展示退火过程是否符合预期 |

### 3. 监督微调(SFT)阶段
| 参数/指标 | 含义 | 必要性 |
|----------|------|--------|
| 指令数据集 | 用于微调的高质量指令数据 | 决定模型的指令遵循能力 |
| 指令数据量 | 微调数据的总条数 | 数据量需平衡，过多过少都有问题 |
| 微调轮次 | 完整遍历数据集的次数 | 避免过拟合同时确保充分学习 |
| 微调学习率 | SFT阶段的学习率，通常比预训练小 | 保持原有知识的同时学习新能力 |
| 微调批次大小 | SFT阶段的batch size | 影响微调效率和稳定性 |
| 领域适配比例 | 特定领域数据在微调集中的占比 | 平衡通用能力和领域专长 |
| 指令遵循评分 | 模型按指令执行的准确性评分 | 衡量微调效果的关键指标 |

### 4. 偏好对齐/强化学习阶段
| 参数/指标 | 含义 | 必要性 |
|----------|------|--------|
| RL算法 | 使用的强化学习算法(PPO、DPO等) | 不同算法适用于不同场景和数据规模 |
| 奖励模型 | 用于评估模型输出质量的评分模型 | 高质量奖励模型是RL成功的关键 |
| 人类偏好数据 | 包含人类偏好判断的数据集 | 确保对齐人类价值观和偏好 |
| KL系数 | 控制新旧策略差异的系数 | 防止过度优化导致灾难性遗忘 |
| 偏好数据量 | 人类偏好判断的数据条数 | 数据质量和多样性影响对齐效果 |
| 奖励分布 | 奖励模型评分的分布情况 | 检测奖励模型是否出现偏见 |
| 行为改善示例 | 展示RL前后回答对比 | 直观展示对齐效果 |

### 5. 蒸馏与压缩阶段
| 参数/指标 | 含义 | 必要性 |
|----------|------|--------|
| 教师模型 | 作为知识来源的大模型 | 教师模型质量决定蒸馏上限 |
| 学生模型 | 接收知识的小模型 | 通常是架构更小的模型 |
| 蒸馏温度 | 控制soft label软硬程度的参数 | 影响知识迁移的细粒度 |
| 蒸馏损失 | 衡量知识迁移效果的损失函数 | 指导学生模型向教师模型学习 |
| 性能保留率 | 与教师模型相比保留的性能百分比 | 衡量蒸馏效果的关键指标 |
| 参数压缩比 | 压缩后与原始参数量的比值 | 量化压缩效果的直观指标 |
| 剪枝方法 | 移除不重要参数的策略 | 影响压缩后模型性能保留率 |

### 6. 量化阶段
| 参数/指标 | 含义 | 必要性 |
|----------|------|--------|
| 量化方法 | 使用的技术(PTQ、QAT等) | 不同方法有不同的精度和复杂度 |
| 位宽 | 量化后的数值精度(如INT8、INT4) | 影响模型大小和推理速度 |
| 校准数据集 | 用于校准量化参数的数据 | 代表性数据确保量化精度 |
| 量化敏感层 | 对量化特别敏感的网络层 | 这些层可能需要特殊处理 |
| 精度损失 | 量化前后性能差异 | 评估量化的影响程度 |
| 加速比 | 量化后的推理速度提升 | 量化的主要目标之一 |
| 内存节省 | 量化后的内存占用减少 | 评估在资源受限设备上的适用性 |

### 7. 系统优化阶段
| 参数/指标 | 含义 | 必要性 |
|----------|------|--------|
| 推理引擎 | 模型部署使用的推理框架 | 不同引擎有不同的优化侧重点 |
| 并行策略 | 模型并行、张量并行等方式 | 影响大模型的推理吞吐量 |
| KV缓存 | 注意力键值对的缓存策略 | 显著影响生成速度 |
| 批处理能力 | 同时处理多请求的能力 | 影响服务效率和成本 |
| 延迟指标 | 请求响应时间 | 用户体验的关键指标 |
| 吞吐量 | 单位时间处理的请求数 | 服务能力的关键指标 |
| 峰值内存 | 推理过程中的最大内存占用 | 影响硬件需求和部署成本 |

### 8. 持续评测阶段
| 参数/指标 | 含义 | 必要性 |
|----------|------|--------|
| 基准测试套件 | 标准评测数据集合(MMLU、GSM8K等) | 提供模型能力的通用衡量标准 |
| 领域评测 | 特定领域的评测(医疗、法律等) | 评估模型在垂直领域的专业能力 |
| 红队测试 | 安全性和鲁棒性测试 | 发现模型的潜在风险和弱点 |
| 人类评估 | 由人类评估模型输出质量 | 提供更主观的质量评价 |
| 基线模型 | 用于对比的参考模型 | 提供性能改进的相对参考 |
| 雷达图 | 多维度能力可视化 | 直观展示模型优劣势 |
| 对抗样本 | 专门设计的具有挑战性的输入 | 测试模型的极限和弱点 |