# Reddit Climate Emotion Polarization Analysis

本项目分析Reddit气候与能源议题讨论中的情绪表达、情感极化与传播热度之间的关系。项目围绕帖子、评论和回复数据，构建从文本清洗、情绪识别、主题建模、极化指标构造到统计建模和机器学习预测的完整分析流程。

## 项目内容

- `full_analysis_pipeline.ipynb`：完整分析流程。
- `outputs/figures/`：图表结果。
- `outputs/tables/`：描述统计、统计模型、机器学习、稳健性检验和图表索引结果。
- `requirements.txt`：运行所需Python包。

## 数据集来源

主数据来自Reddit气候与能源相关subreddit的帖子、评论和回复数据。运行项目时，请将主数据文件命名为：

```text
主数据集/comment.parquet
```

该数据文件体积较大，公开仓库中只保留代码、说明、图表和结果表。

## 情绪数据与模型

项目使用GoEmotions标签体系和情绪映射文件。运行时请准备以下文件：

```text
GoEmotions/train.tsv
GoEmotions/dev.tsv
GoEmotions/test.tsv
GoEmotions/emotions.txt
GoEmotions/sentiment_mapping.json
GoEmotions/ekman_mapping.json
```

情绪识别模型使用：

```text
SamLowe/roberta-base-go_emotions
```

运行前请将模型文件放入：

```text
model_cache/roberta-base-go_emotions/
```

模型权重文件较大，公开仓库中只说明模型名称和放置路径。

## 运行方式

安装依赖：

```bash
pip install -r requirements.txt
```

然后打开并从上到下运行：

```text
full_analysis_pipeline.ipynb
```

Notebook内所有路径都基于项目根目录计算。运行前请确认主数据、GoEmotions文件和本地情绪模型已经按上文路径放好。

## 分析流程

```text
数据读取
→评论与回复展开
→文本清洗
→GoEmotions情绪识别
→TF-IDF+NMF主题建模
→帖子层情感极化指标
→传播热度指标与建模数据集
→描述统计表
→统计建模
→机器学习训练
→稳健性检验
→结果可视化与图表导出
→完整性检查
```

## 输出结果

图表结果位于：

```text
outputs/figures/
```

表格结果位于：

```text
outputs/tables/
```

其中`outputs/tables/figure_index.csv`记录全部正式图表的文件路径、标题和图表类型。

## 数据文件与编码

- 主数据：`主数据集/comment.parquet`，Parquet格式。
- GoEmotions标注文件：`GoEmotions/*.tsv`，UTF-8编码，制表符分隔。
- 情绪映射文件：`GoEmotions/*.json`，UTF-8编码。
- 结果表格：`outputs/tables/*.csv`，UTF-8-SIG编码。
- 结果图表：`outputs/figures/*.png`。
- 中间数据：`processed_data/*.parquet`，由notebook运行生成。

## 解释边界

本项目是观察性分析和预测性分析。Redditupvotes、评论数和回复数反映平台内部互动强度，不等同于真实曝光量。统计模型和机器学习结果用于解释相关关系和预测模式，不用于严格因果推断。
