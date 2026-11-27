# 连续圆角
普通圆角由直线和圆弧组成，切线连续 G1，但曲率从 0 突变到 1/r。连续圆角追求平滑曲率过渡（G2），更自然。Squircle/超椭圆是近似而非苹果精确算法。
数学：|x/a|^n + |y/b|^n = 1；n=2 为椭圆，n=4 或 5 更方，n 越大越接近矩形。
同心圆弧：外半径=内半径+内边距；连续圆角可参考此近似。例：32px 外角、12px padding、20px 内角。
标签 6–8，输入 10–12，按钮 10–14，菜单 12–16，小卡片 12–18，普通卡片 20–24，大卡片/弹窗 24–32，胶囊 9999px。
CSS border-radius + corner-shape: squircle（渐进增强，注意兼容性）；SVG 超椭圆路径 可实现平滑路径。SwiftUI RoundedRectangle(cornerRadius: 24, style: .continuous)。
不要所有元素使用相同半径。