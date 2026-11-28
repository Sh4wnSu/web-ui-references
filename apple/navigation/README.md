# Apple-inspired Navigation
官方参考：Finder（分组、半透明、弱选中背景）、Music（内容分组、主题色）、System Settings（彩色功能图标）、Xcode（紧凑树形导航）、iPadOS（悬浮顶部胶囊）、Safari（紧凑多任务标签）、Health（分段控件）、App Store Connect（下划线标签）、visionOS（悬浮 ornament）。
SwiftUI sidebarAdaptable 可在适合的平台转换侧栏与顶部导航。普通导航尽量不超过两级，更深结构采用 Split View；文件树属于例外。
## 六种侧栏
|类型|背景/选中|用途|
|---|---|---|
|经典 macOS|#e9e9ed / #d4d4da|管理、文件|
|悬浮|#fff / #e8edf6|SaaS|
|玻璃|半透明白 / 高透明白填充|媒体|
|深色|#242426 / #3a3a3e|开发工具|
|极简强调色|#fff / #e7f0ff|统计|
|图标栏|#f0f0f4 / #fff|多面板|
## 八种顶部标签
Segmented（共享底座）、Floating Pill（悬浮胶囊）、Underline（下划线）、Filled（独立填充）、Glass（玻璃）、Compact（Safari 紧凑）、Icon + Text（图文）、Top Indicator（顶部指示线）。
页面导航使用链接和 aria-current；内容面板使用 tablist/tab/tabpanel；周期或筛选使用分段选择。支持方向键、Home/End、焦点及减少动效。
## 三种组合
A macOS Dashboard：灰侧栏、白内容、分段二级导航。
B Glass Workspace：环境渐变、悬浮玻璃侧栏与胶囊、实色或高不透明内容。
C Professional Workspace：紧凑侧栏、顶部工具栏、下划线二级标签；适合 AI Agent 与开发工具。
## 推荐 Web 参数
侧栏 220–260px，紧凑 180–220px，图标 52–64px；行高 32–40px，圆角 7–10px，悬浮 20–28px；图标 16–20px，文字 13–14px，选中 500–600，分组 11–12px，组间距 20–28px，图文间距 8–10px；折叠 200–300ms，模糊 20–32px。
Tab 高 32–44px，分段 30–36px，文字 13–15px，水平 padding 12–20px，容器 3–4px，选中圆角 7–10px 或胶囊，下划线 2px，滑动 180–280ms，阴影 0 1px 4px #00000014。
以上为 Web 建议，不是苹果官方固定尺寸。玻璃为 CSS 近似，不是真实折射。
[源码资源](source-catalog.md) · [交互图库](../../examples/navigation/index.html) · [Tokens](../../design-tokens/navigation.css)

[Spring 动效与侧栏动画编排](motion/README.md)

[独立胶囊滑块与 Spring 动效](../capsule-controls/README.md)

[侧边栏底部账号与连续圆角菜单](account/README.md)
