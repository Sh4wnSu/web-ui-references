# 可访问性
优先原生 table/caption/thead/tbody/th scope；排序按钮 aria-sort 放在 th；多选使用带名称的 checkbox，支持 indeterminate；展开按钮 aria-expanded；分组设置使用 dl。不要随意将普通 table 改为 grid；真正交互式 grid 需实现键盘导航。焦点可见，状态不只靠颜色，玻璃提供不透明降级。