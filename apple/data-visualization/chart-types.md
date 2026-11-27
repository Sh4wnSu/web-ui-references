# 图表分类与选型
分类非唯一标准，部分图表跨类别。以下 66 个条目包含图表及 KPI 展示组件。
|类别|图表（英文）|用途|
|---|---|---|
|趋势|折线 Line|连续趋势|
|趋势|面积 Area|趋势与规模|
|趋势|多折线 Multi-line|多指标趋势|
|趋势|堆叠面积 Stacked Area|总量及组成变化|
|趋势|迷你趋势 Sparkline|卡片及表格|
|趋势|阶梯 Step|价格及状态变化|
|趋势|带状区间 Band|预测、置信区间|
|趋势|蜡烛 Candlestick|OHLC|
|比较|柱状 Column|类别大小|
|比较|横向条形 Bar|排名、长名称|
|比较|分组柱 Grouped Bar|多系列比较|
|比较|堆叠柱 Stacked Bar|总量与组成|
|比较|百分比堆叠 100% Stacked|组成比例|
|比较|棒棒糖 Lollipop|轻量排名|
|比较|哑铃 Dumbbell|前后差异|
|比较|斜率 Slope|两时间点变化|
|组成|饼 Pie|少量类别占比|
|组成|环形 Donut|占比与中心汇总|
|组成|容量条 Capacity Bar|磁盘、显存、费用|
|组成|矩形树 Treemap|层级占比|
|组成|华夫饼 Waffle|百分比|
|组成|旭日 Sunburst|多层级组成|
|分布|直方 Histogram|频率分布|
|分布|箱线 Box Plot|中位数、四分位数、异常值|
|分布|小提琴 Violin|分布密度|
|分布|密度 Density|概率密度|
|分布|蜂群 Beeswarm|观测样本|
|分布|山脊 Ridgeline|多组分布|
|关联|散点 Scatter|双变量相关|
|关联|气泡 Bubble|三维数值|
|关联|相关矩阵 Correlation Matrix|两两关联|
|关联|平行坐标 Parallel Coordinates|高维比较|
|进度|进度条 Progress Bar|完成度|
|进度|进度环 Progress Ring|配额、目标|
|进度|活动环 Activity Rings|多个目标|
|进度|仪表 Gauge|实时阈值|
|进度|子弹 Bullet|实际、目标、评价区间|
|进度|液位 Liquid Fill|容量|
|区间时间|区间条 Range Bar|最小最大值|
|区间时间|误差棒 Error Bar|不确定性|
|区间时间|甘特 Gantt|任务周期|
|区间时间|状态时间线 State Timeline|状态持续时间|
|区间时间|瀑布 Waterfall|累计增减|
|区间时间|时间轴 Timeline|里程碑|
|矩阵|热力 Heatmap|二维强度|
|矩阵|日历热力 Calendar Heatmap|每日活动|
|矩阵|二维密度 2D Density|聚集区域|
|矩阵|频谱 Spectrogram|时间频率能量|
|流程层级|桑基 Sankey|资源流向|
|流程层级|漏斗 Funnel|转化流失|
|流程层级|树状 Tree|层级|
|流程层级|网络 Network|依赖关系|
|流程层级|弦 Chord|相互流向|
|流程层级|圆形打包 Circle Packing|层级规模|
|多维|雷达 Radar|多能力维度|
|多维|极坐标柱 Polar Bar|周期、方向|
|多维|玫瑰 Rose|周期规模|
|多维|小多图 Small Multiples|独立图表比较|
|地理|分级着色 Choropleth|区域数值（宜归一化）|
|地理|气泡地图 Bubble Map|位置与规模|
|地理|地理热力 Geographic Heatmap|空间密度|
|地理|流向地图 Flow Map|跨区域流量|
|混合|KPI Metric Card|核心数字|
|混合|KPI + Sparkline|数字及趋势|
|混合|柱线组合 Combination|相关指标|
|混合|表格内图 In-cell Charts|精确值及趋势|
## 33 项核心组件路线
P0（10）：KPI Card、Sparkline、Line、Area、Bar、Stacked Bar、Donut、Capacity Bar、Progress Ring、Data Table。
P1（12）：Activity Rings、Range Bar、Band、Heatmap、Calendar Heatmap、Histogram、Box Plot、Scatter、Bullet、State Timeline、Waterfall、Funnel。
P2（11）：Sankey、Treemap、Sunburst、Radar、Gantt、Network、Violin、Bubble、Chord、Parallel Coordinates、Geographic Map。
AI 服务监控优先：面积折线（吞吐/请求）、KPI（核心指标）、堆叠柱（模型费用）、区间（TTFT/速度）、容量条（显存/配额）、箱线（稳定性）、状态时间线（Agent）、热力（并发）、散点（成本性能）、桑基（调度流向）。
