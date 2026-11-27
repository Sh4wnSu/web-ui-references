# 图表配色方案 A / B / C

A 为传统 Apple 系统色参考，适合语义明确的指标；B 为自定义柔和色板，适合多图表桌面 Dashboard；C 为自定义单色阶，适合有序数据和关联系列。并非苹果官方统一图表色板。

|颜色|A 系统色|B 柔和色|
|---|---|---|
|blue|#007AFF|#6389C6|
|green|#34C759|#68A68C|
|orange|#FF9500|#D5A16B|
|Red / Rose|#FF3B30|#CC7882|
|purple|#AF52DE|#9C85BE|
|indigo|#5856D6|#7D8DBB|
|cyan|#5AC8FA|#69AAB5|
|yellow|#FFCC00|#CCB66C|

## C 单色系

|色相|0.35|0.45|0.55|0.65|0.75|0.85|
|---|---|---|---|---|---|---|
|245°|oklch(0.35 .08 245)|oklch(0.45 .08 245)|oklch(0.55 .08 245)|oklch(0.65 .08 245)|oklch(0.75 .08 245)|oklch(0.85 .08 245)|
|155°|oklch(0.35 .08 155)|oklch(0.45 .08 155)|oklch(0.55 .08 155)|oklch(0.65 .08 155)|oklch(0.75 .08 155)|oklch(0.85 .08 155)|
|300°|oklch(0.35 .08 300)|oklch(0.45 .08 300)|oklch(0.55 .08 300)|oklch(0.65 .08 300)|oklch(0.75 .08 300)|oklch(0.85 .08 300)|
|50°|oklch(0.35 .08 50)|oklch(0.45 .08 50)|oklch(0.55 .08 50)|oklch(0.65 .08 50)|oklch(0.75 .08 50)|oklch(0.85 .08 50)|

C 固定色度 .08，改变感知明度；色相 245 蓝、155 绿、300 紫、50 暖橙。需进行色域及对比度检查；有序色阶不适合无序类别过多的情况。深浅主题应分别验证，不能仅靠颜色传递状态。A 的传统浅色参考值不是动态系统色的完整替代。

[CSS](../../design-tokens/chart-palettes.css) · [JSON](../../design-tokens/chart-palettes.json) · [可视化示例](../../examples/chart-palettes/index.html)

使用：在容器设置 data-chart-palette="system"、"muted" 或 "mono-245"（亦可 155/300/50），图表读取 --chart-series-1 等变量。