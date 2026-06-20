# U20国青智能助教 MVP

## 项目目标

开发一套基于比赛数据分析的足球青训辅助系统。

用户输入比赛统计数据后，系统自动：

* 分析比赛表现
* 对标世界U20强队
* 识别短板
* 输出训练建议
* 生成教练报告

---

# 技术栈

## 后端

* Python 3.12
* FastAPI
* SQLAlchemy
* SQLite（MVP）
* PostgreSQL（生产环境）

## 数据分析

* Pandas
* NumPy

## AI分析

* OpenAI API
* DeepSeek API（可选）

## 图表

* Plotly
* Matplotlib

## PDF导出

* ReportLab

---

# 项目结构

```text
u20-assistant/

├── app.py
├── requirements.txt
├── config.py
│
├── database/
│   ├── models.py
│   ├── db.py
│   └── seed.py
│
├── analysis/
│   ├── benchmark.py
│   ├── compare.py
│   ├── diagnosis.py
│   ├── report.py
│   └── training_plan.py
│
├── charts/
│   ├── radar.py
│   └── trend.py
│
├── api/
│   ├── match.py
│   ├── report.py
│   └── benchmark.py
│
├── pdf/
│   └── exporter.py
│
├── templates/
│   └── report_template.html
│
└── data/
    └── benchmark.json
```

---

# 数据模型

## Match

```python
class Match:
    id: int
    opponent: str
    result: str

    possession: float
    shots: int
    shots_on_target: int

    xg: float
    xga: float

    high_intensity_run: float
    total_distance: float

    pass_accuracy: float
    key_passes: int

    created_at: datetime
```

---

# 世界基准数据

```json
{
  "worldClass": {
    "possession": 56,
    "shots": 14,
    "shotsOnTarget": 6,
    "xG": 1.9,
    "xGA": 0.9,
    "highIntensityRun": 10.5,
    "totalDistance": 108,
    "passAccuracy": 86,
    "keyPasses": 12
  }
}
```

---

# 功能一：比赛录入

## 输入字段

* 对手
* 比赛结果
* 控球率
* 射门次数
* 射正次数
* xG
* xGA
* 高强度跑动
* 总跑动距离
* 传球成功率
* 关键传球

---

# 功能二：数据对比

## 输出

```json
{
  "possessionGap": -11,
  "shotsGap": -7,
  "xGGap": -1.1,
  "keyPassGap": -8
}
```

---

# 功能三：自动诊断

## 规则

### 进攻创造力

```python
if xg < 1:
    issue = "进攻创造力不足"
```

### 压迫强度

```python
if high_intensity_run < 8:
    issue = "高位压迫不足"
```

### 传控能力

```python
if pass_accuracy < 80:
    issue = "传球稳定性不足"
```

---

# 功能四：训练建议引擎

## 输出模板

```text
训练建议：

1. 高位压迫训练
2. 肋部渗透训练
3. 快速攻防转换训练
4. 小范围传控训练
```

---

# 功能五：AI比赛报告

## Prompt

```text
你是一名职业足球数据分析师。

请根据以下比赛数据：

{match_data}

输出：

1. 比赛总结
2. 优势分析
3. 问题分析
4. 训练建议

字数控制在300字以内。
```

---

# 功能六：雷达图

## 指标

* 控球率
* 射门
* 射正
* xG
* 高强度跑动
* 传球成功率
* 关键传球

比较对象：

* 当前比赛
* 中国U20均值
* 世界U20均值

---

# 功能七：趋势分析

展示最近：

* 5场比赛
* 10场比赛
* 赛季全部比赛

趋势指标：

* xG
* xGA
* 控球率
* 射门
* 跑动距离

---

# 功能八：PDF导出

生成内容：

* 封面
* 比赛信息
* 雷达图
* 趋势图
* AI分析报告
* 训练建议

导出格式：

```text
U20_Report_2026_06_20.pdf
```

---

# REST API

## 新增比赛

```http
POST /api/matches
```

## 获取比赛

```http
GET /api/matches
```

## 获取单场比赛

```http
GET /api/matches/{id}
```

## 生成报告

```http
POST /api/report/{id}
```

## 导出PDF

```http
GET /api/export/{id}
```

---

# MVP阶段目标

实现：

* 比赛录入
* 数据库存储
* 世界基准对比
* 自动诊断
* AI报告生成
* 雷达图
* PDF导出

预计代码量：

```text
2000~3000行Python
```

预计开发时间：

```text
1~2周
```

适用对象：

* 青训教练
* 校园足球
* U15/U17/U20梯队
* 足球培训机构
