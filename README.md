# 月度销售数据监控仪表盘

本项目基于 **Excel + Power Query   Excel电源查询Excel   Power Query   Excel电源查询** 构建了一个自动化的销售数据监控仪表盘，用于分析月度成交金额、客户数、客单价及环比趋势，并支持按区域、省份、产品期数下钻。通过将新的每日销售明细和销售人员信息放入指定文件夹，即可一键刷新报表，无需手动修改公式。

## 📊 功能特性

- **自动数据整合**  
  使用 Power Query 合并多个月份的每日成交汇总表，并与销售人员表关联，自动补充区域、省份、职务类别等维度。

- **历史数据滚动更新**  
  保留历史数据，新增月份数据只需放到 `数据处理` 文件夹，刷新即可追加到总模型中。

- **交互式仪表盘**  
  - 主指标卡片：成交金额、客户数、客单价及其环比  
  - 省份明细表：自动计算各省份的金额、客户数、客单价及环比（使用 `GETPIVOTDATA` 动态获取）  
  - 产品期数分析：不同期数产品的成交占比及环比趋势  
  - 区域成交趋势图：基于数据透视表的动态图表  

- **动态公式**  
  综合运用 `VLOOKUP`、`MATCH   匹配`、`INDEX   指数`、`GETPIVOTDATA` 等函数，实现筛选联动和指标自动计算。

## 📁 文件结构
项目文件夹/
├── 月度销售数据监控.xlsx # 主工作簿（包含所有工作表、Power Query 连接）
├── 数据源/
│ ├── 6月_每日销售成交汇总数据.xlsx # 示例：6月每日数据
│ ├── xx月_每日销售成交汇总.xlsx # xx月每日数据
│ └── 销售人员表-截止7月1日.xlsx # 最新的人员信息表
└── README.md # 本文件


**主工作簿包含以下工作表：**
- `源数据`：Power Query 加载并合并后的全量销售明细  
- `中间表-数据`：基于源数据生成的数据透视表（汇总区域、省份、期数等）  
- `中间表-图表`：供图表使用的辅助透视表（日趋势、期数分布）  
- `仪表盘`：主看板（占位，可扩展）  
- `阅读成交仪表盘`：最终可视化仪表盘，包含所有图表和指标  

## 🔄 数据处理流程

A[每日销售汇总文件] -->|Power Query 合并| B(全量销售明细)
C[销售人员表] -->|Power Query 关联| BC[销售人员表] -->|Power Query 关联| BC[销售人员表] -->|Power Query 关联| BC[销售人员表] -->|Power Query 关联| B
B --> D[数据透视表 + 计算列]
D --> E[仪表盘公式引用]
E --> F[动态图表 & 指标]

Power Query 数据获取

从 数据源 文件夹中读取所有 *_每日销售成交汇总.xlsx 文件，追加合并为一张表。

读取 销售人员表.xlsx，与销售明细按 销售工号 左连接，补充区域、省份、职务类别等信息。

将结果加载到 源数据 工作表。

数据建模

在 源数据 基础上创建多个数据透视表（中间表-数据、中间表-图表），计算成交金额、客户数、客单价及月环比。

使用 GETPIVOTDATA 从透视表中提取动态指标，避免硬引用。

可视化

仪表盘单元格使用 VLOOKUP + MATCH 实现行列双向查找。

环比数据通过 IFERROR + GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。环比数据通过 IFERROR   GETPIVOTDATA 安全获取。

图表直接绑定透视表区域，自动随筛选器更新。

🚀 如何使用
1. 初始化设置
将项目文件夹放置于本地路径（例如 D:\SalesDashboard）。

确保主工作簿 月度销售数据监控.xlsx 与 数据源 文件夹在同一目录下。

2. 添加新月份数据
准备下个月的每日销售汇总文件，命名格式建议：MM_每日销售成交汇总.xlsx（例如 7月_每日销售成交汇总.xlsx）。

将该文件放入数据处理文件夹。

注意：文件内列名必须与现有文件一致（成交日期、销售工号、产品、成交金额、成交客户数）。

3. 更新销售人员信息
将最新的 销售人员表.xlsx 替换 数据处理 文件夹中的旧文件。

保持列名一致（销售工号、入职时间、离职时间、职务类别、所属小组、所属省份、所属区域）。

4. 刷新数据
打开 月度销售数据监控.xlsx。

在 Excel 中点击 数据 → 全部刷新（或按 Ctrl+Alt+F5）。

Power Query 会自动检测文件夹中的变化，合并新数据并刷新所有透视表和图表。

5. 查看仪表盘
切换到 阅读成交仪表盘 工作表。

使用切片器（如有）或直接修改月份筛选器，所有指标和图表将自动更新。

🛠 技术栈
组件	用途
Power Query	数据导入、合并、追加、关联销售人员表
数据透视表	快速分组汇总（区域、省份、期数、日期）及环比计算
公式	VLOOKUP、MATCH、INDEX 实现动态查找
GETPIVOTDATA 精确获取透视表值
IFERROR 处理缺失环比
图表	折线图（区域成交趋势）、饼图/条形图（产品期数占比）
📌 注意事项
文件命名：每日销售汇总文件必须包含 每日销售成交汇总 字样，否则 Power Query 不会识别。

列名一致性：所有源文件的列名（英文或中文）必须与示例文件完全一致，否则刷新会报错。

销售人员表：离职人员建议保留但标记离职时间，Power Query 可以根据需要过滤。

环比计算：依赖前一月份的数据存在，若新增月份为首月，环比会显示为空（或错误值），可手动处理。

性能优化：数据量较大时，建议将 Power Query 的加载目标设置为“仅连接”，透视表基于 源数据 表建立。

🔧 自定义扩展
增加新维度：在 销售人员表 中添加列（如城市、渠道），然后在 Power Query 中合并到明细，刷新透视表即可。

修改图表类型：直接选中图表区域，更改图表类型或数据源。

添加新的 KPI：在 阅读成交仪表盘 中插入新单元格，使用 GETPIVOTDATA 引用透视表字段。

📄 示例数据说明
提供的示例数据为6月的销售记录，以及截至7月1日 的销售人员信息。所有数据均为模拟脱敏数据，仅用于演示仪表盘功能。

🤝 贡献
欢迎提交 Issue 或 Pull Request 改进数据模型或可视化样式。

📧 联系方式
如有疑问，请联系项目维护者。

