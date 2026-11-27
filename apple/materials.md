# 材质、阴影与边框
Flat：背景差或 1px 弱边框；Raised：0 2px 8px rgba(0,0,0,.04)；Floating：0 16px 48px rgba(0,0,0,.12) + 0 4px 12px rgba(0,0,0,.05)。避免同时叠加强边框和阴影。
Frosted Glass 依靠背景模糊、半透明和饱和度。Liquid Glass 更强调环境响应、边缘高光、折射与动态形变，适合导航控制层，不应覆盖所有内容。
CSS 近似：background: rgba(255,255,255,.65); backdrop-filter: blur(20px) saturate(160%); border: 1px solid rgba(255,255,255,.5)。这不是真实光学折射；高级实现可研究 SVG filter/WebGL。提供不透明降级和可读性保护。