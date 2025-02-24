# OpenSearch-SQL

一个完整的Text-to-SQL框架, 2024年8月在[BIRD](https://bird-bench.github.io/)上取得第一名。下面是完整的流程图

<p align="center">
  <img src="./image/overview3.jpg" alt="image" />
</p>
<div align="center">
  
[📖 Arxiv](https://arxiv.org/abs/2502.14913) |
中文版 |
[英文版]()

</div>

## Text-to-SQL

Text-to-SQL任务的目标是使从业人员不必掌握专门的数据库技能，它将用户的自然语言描述转化为SQL查询来完成用户的需求。比如：

**User Query**:
```
"What is the tallest building?"
```
**SQL Query**:
```sql
SELECT building_name FROM buildings ORDER BY height DESC LIMIT 1
```

## Overview
OpenSearch-SQL通过Preprocessing、Extraction、Generation、Refinement以及Alignment模块组成。
整个OpenSearch-SQL框架运行不依赖于额外训练，你可以使用GPT、DeepSeek、Gemini等模型完成工作。

除了Schemelinking、BeamSearch采样生成答案和Self-Consistnecy \& vote 之外，我们依赖独特的框架设计取得了效果的提升。

1. 在OpenSearch-SQL中，我们第一次提出了Self-taught的CoT补充方法，将Query-SQL Pair形式的Few-shot扩展成Query-CoT-SQL Pair，这大大提升了模型表现。
2. 我们为Text-to-SQL人物设计了一种结构化的CoT思路，并设计了SQL-Like的中间语言来优化SQL生成
3. 除此之外，我们第一次提出了Alignment方法，将Agent的输入输出进行对齐，这缓解了模型幻觉的问题。
例如：不同数据集的风格要求、Agent信息传递的幻觉、生成SQL的基本逻辑问题
4. 在提交时，我们在BIRD的三个榜单上都取得了第一：验证集上69.3%的EX，测试集上72.28%的EX，69.36%的R-VES.
<p align="center">
  <img src="./image/bird_ranl.jpg" alt="image" />
</p>


# Run

**installation**：

```shell
pip install -r requirements.txt
```
**Data processing**：
   ```bash
   sh run/run_preprocess.sh  # 每个目录的输出见控制台输出，处理fewshot，table 等数据
   ```
你也可以直接使用在Bird路径下的fewshot

**Main**：
   ```bash
   sh run/run_main.sh  # ，path：src/runner/database_manager.py-> _set_paths
   ```
   