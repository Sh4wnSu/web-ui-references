# 动效与可访问性
Hover 120–180ms；Press 80–120ms、scale(.97–.98)；开关 180–250；菜单 150–250；Tab 200–300；卡片展开/弹窗 250–400；页面 300–450ms。
标准 cubic-bezier(.25,.1,.25,1)，ease-out (.22,1,.36,1)，弹性近似 (.34,1.56,.64,1)。真实弹簧需要物理模型。原生 Web Animations API 可实现复杂动效；官网可用 sticky、视差、滚动序列。
动效解释状态和空间关系，不为装饰而运动。支持 prefers-reduced-motion、键盘 Tab/Enter/Esc、可见焦点、语义 HTML、字体放大、对比度及不透明降级。
[Apple-inspired Spring 专题](navigation/motion/README.md)
