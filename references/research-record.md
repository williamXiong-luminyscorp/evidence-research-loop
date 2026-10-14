# 研究记录与恢复

开始一轮研究或跨会话恢复时读取。优先沿用现有项目记录格式，避免重复建档。没有现成结构时，在用户工作区创建一个有明确名称的研究目录；每轮使用独立 ID，保存以下逻辑产物即可，不要求额外平台。

| 产物 | 最少记录内容 |
| --- | --- |
| 状态记录 | 用户目标、范围、阶段状态、已完成证据、待做工作、阻碍、下一条具体执行命令 |
| 文献表 | 来源 ID/URL、检索日期、文献类型、实际阅读范围、样本/方法、发现、局限、对应假设 |
| 实验协议 | 研究问题、比较单位、候选/基线、输入输出、主要指标、错误条件、标签来源、数据划分、统计/选择规则、重复次数、预算、停止条件 |
| 候选档案 | ID、父方案、作者/模型、机制、来源 ID、实现路径/哈希、改动理由、开发集结果、入围或淘汰原因 |
| 运行档案 | 命令、时间、退出状态、程序/数据/配置版本、模型/种子（不可获则写未知）、原始输出、程序评分、耗时/成本及其测量口径 |
| 冻结记录 | 冻结时间、协议/裁判/数据/候选哈希、入围规则、测试访问记录、修订历史 |
| 结果报告 | 全部对照、改进前后、独立测试、消融、失败、结论、限制、下一步 |

可将状态记录实现为 JSON/YAML，或放在已有报告中。下面是字段约定，不是预先完成的结果：

```yaml
research_id: null
user_decision: null
scope: null
data_provenance: null
protocol_path: null
protocol_hash: null
comparison_unit: null
primary_metric: null
budget_and_stop_rule: null
stages:
  literature: {status: not_started, evidence: []}
  protocol_and_judge: {status: not_started, evidence: []}
  proposals: {status: not_started, evidence: []}
  development_comparison: {status: not_started, evidence: []}
  failure_driven_iteration: {status: not_started, evidence: []}
  freeze: {status: not_started, evidence: []}
  independent_test: {status: not_started, evidence: []}
  ablation: {status: not_started, evidence: []}
  conclusion: {status: not_started, evidence: []}
unresolved_limits: []
next_action: null
```

状态可用 `not_started / running / completed / partial / blocked`。阶段完成必须附真实证据路径；`not_applicable` 只用于协议说明不适用或用户明确排除的步骤，保留原因，不能绕过必要比较。不存在失败时记录实际观察和停止理由，不人为制造失败。

恢复时先核对记录指向的文件确实存在、版本是否一致。已有测试集一旦被用来改进方案，就失去未见性质。对新材料、新方案或新的研究问题，明确哪些既有结果仍适用、哪些必须重新运行。

报告中的结果表至少列出方案、集合、独立案例数、运行次数、主要指标、严重错误、失败/缺失、成本和证据路径。将“已执行的结果”和“待执行的验收/实验”分开。能复算分数不意味着标签真实或研究设计有效；这些需分别说明。
