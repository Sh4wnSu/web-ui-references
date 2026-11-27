# 滑块动效
单一绝对定位滑块独立于按钮，通过测量目标按钮的位置和宽度更新 transform/width。固定等宽可以只用 translateX。自适应宽度需 ResizeObserver。
推荐 Spring k=500,c=40,m=1，阻尼比约 .89；可复用 spring.json 的其他预设。保留位置、宽度及各自速度以支持连续反向点击。CSS 近似 cubic-bezier(.22,1.25,.36,1) 350ms 不是真实物理弹簧。
React Motion: 在选中按钮内渲染 <motion.span layoutId="active-capsule" transition={{type:"spring",stiffness:500,damping:40,mass:1}} />；每组使用独立 LayoutGroup/id，避免跨控件共享。按压反馈 scale(.97)，可选轻微拉伸回缩，不应让文字一起变形。尊重 prefers-reduced-motion。真实液态折射需额外渲染技术，本示例不实现。