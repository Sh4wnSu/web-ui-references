# 自适应色彩系统（Adaptive Color System）

## 1. Apple Music 的公开依据与边界
Apple Music 根据封面形成协调的环境背景：保留色相、控制色度和明度、多色融合、柔化空间细节、平滑切换。内部播放界面算法未公开，以下是可复现的 Web 方案而非逆向结论。
[Artwork](https://developer.apple.com/documentation/applemusicapi/artwork) 提供 bgColor（平均背景色）和 textColor1–4（四级文字色）；MusicKit 也提供相关数据。它们不一定是播放背景实际使用的参数。
官方示例色板：#0b1b18 / #fc977a / #ef5429 / #cc7e66 / #c14925；#e1b73e / #0d0d0c / #232323 / #382f16 / #494128。
Core Image 提供 CIAreaAverage、CIAreaHistogram、CIKMeans、CIPaletteCentroid、CIPalettize、CIColumnAverage、CIRowAverage。CIKMeans 输出聚类中心及权重。参考 [Accelerate 主色提取示例](https://developer.apple.com/documentation/accelerate/calculating-the-dominant-colors-in-an-image)、[Core Image](https://developer.apple.com/documentation/coreimage)、[MusicKit](https://developer.apple.com/documentation/musickit)。

## 2. 处理流水线
原图 → 缩小/透明像素处理 → 颜色提取 → 代表色评分与去重 → OKLCH 映射 → 色域压缩 → 渐变/颜色场 → Scrim 与玻璃染色 → 对比度验证 → 缓存与渲染。
|算法|特点|适用|
|---|---|---|
|Average|极快，互补色易混灰|占位|
|Dominant|最大颜色，忽略特色小区域|单色背景|
|Median Cut|量化代表色|通用主题|
|K-Means|聚类中心及权重|精细主题|
|空间采样|保留色彩位置|多色渐变|
|原图模糊|自然但明度难控制|沉浸播放器|
建议 K-Means + 空间采样；在 OKLab 中计算聚类距离。评分示例 Score = w^0.65 × f(C) × g(L)，w 为面积占比，f 抑制无意义灰白黑和过高色度，g 抑制极端明度。按感知距离去重。黑白图保持中性；不可强行染色。评分函数是启发式，需按素材验证。

## 3. OKLCH 感知映射
L 感知明度、C 色度、H 色相。HSL 的相同明度/饱和度并不意味着相同视觉亮度。保留 H，使用 C'=min(C×0.45,Cmax)，而非强制固定 C。对超出 sRGB 的颜色降低色度至入色域。
|用途|L|C|
|---|---|---|
|浅色页面|.94–.98|.008–.025|
|浅色卡片|.86–.95|.015–.045|
|浅色玻璃|.88–.98|.010–.035|
|深色页面|.18–.28|.015–.045|
|深色卡片|.28–.40|.025–.065|
|音乐背景|.28–.58|.035–.090|
|渐变光晕|.45–.70|.060–.120|
|强调色|.50–.75|.100–.220|
以上是推荐范围而非官方参数。语义色板参考：Base L=.23 C=.025；Surface .34/.045；Elevated .46/.065；Accent .63/.09；Tint .90/.025。实际色度不得超过原图映射值；灰图保留 C≈0。强调色与背景色可采用不同压缩比例。

## 4. 背景生成
### 原图模糊
```css
.artwork-background {
 position:absolute; inset:-15%; background-image:var(--artwork);
 background-size:cover; background-position:center;
 filter:blur(80px) saturate(.6) brightness(.75);
 transform:scale(1.2);
}
```
父容器裁剪溢出；叠加独立遮罩。优点是保留空间关系，缺点是不同封面明度不稳定。
### 多重径向渐变（默认推荐）
```css
.ambient-background {
 background:
 radial-gradient(ellipse at 15% 10%,var(--color-1),transparent 65%),
 radial-gradient(ellipse at 90% 15%,var(--color-2),transparent 65%),
 radial-gradient(ellipse at 55% 100%,var(--color-3),transparent 70%),
 var(--base-color);
}
```
提取 3–4 色，位置可来自聚类空间质心。控制重叠、亮度与文字区域。
### Mesh Gradient
SwiftUI 提供 MeshGradient；Web 可用多径向渐变、SVG 近似、Canvas 2D、WebGL shader 或 WebGPU。缓慢移动控制点产生流体效果；不要频繁全屏重绘。
### 低分辨率颜色场
将图像缩小至 3×3、4×4 或 8×8，逐格 OKLCH 映射，再平滑放大和模糊。保留空间位置、去除纹理。可用 Canvas 预渲染并缓存。

## 5. 玻璃材质与可读性
分层：环境背景 → backdrop blur → 主题 tint → 半透明表面 → 边缘高光。Scrim 独立控制背景明度。
```css
.glass {
 background:color-mix(in oklch,var(--theme-tint) 20%,transparent);
 backdrop-filter:blur(24px) saturate(125%);
 border:1px solid rgb(255 255 255 / 18%);
 box-shadow:inset 0 1px 0 rgb(255 255 255 / 15%),0 8px 32px rgb(0 0 0 / 8%);
}
```
Vibrancy 是环境适配前景的理念，Web 只能近似：一级文字白/近黑，二三级文字按实际合成背景计算对比度，图标继承文字色，激活用强调色。WCAG 普通文字 4.5:1、大字 3:1；渐变须检查文字覆盖区域最差点，而非仅检查平均色。必要时增加遮罩或不透明底板。提供减少透明度及减少动效的替代。

## 6. 图片适配
鲜艳图限制色度；暖色图避免过黄棕；冷色图统一视觉明度；黑白图保持无彩色；互补色保留不同区域而非直接平均。适用于音乐、影视海报、相册、头像主题、商品详情和壁纸工作台。

## 7. 库与实现
[Color Thief](https://github.com/lokesh/color-thief)、[Vibrant.js](https://github.com/Vibrant-Colors/node-vibrant)、[Color.js](https://github.com/color-js/color.js)、[Culori](https://github.com/Evercoder/culori)、[Fast Average Color](https://github.com/fast-average-color/fast-average-color)、[Material Color Utilities](https://github.com/material-foundation/material-color-utilities)、[Quantize](https://github.com/lokesh/quantize)。
Vibrant.js 提供 Vibrant、Light Vibrant、Dark Vibrant、Muted、Light Muted、Dark Muted 六类色板。
参考依赖方案（版本 API 需核对，未运行验证）：
```js
import ColorThief from "colorthief";
import {converter,formatHex,toGamut} from "culori";
const toOKLCH=converter("oklch"), mapToRGB=toGamut("rgb");
function mapColor(rgb,l,max){
 const color=toOKLCH({mode:"rgb",r:rgb[0]/255,g:rgb[1]/255,b:rgb[2]/255});
 return formatHex(mapToRGB({mode:"oklch",l,c:Math.min(color.c*.45,max),h:color.h}));
}
export async function generateTheme(image){
 await image.decode();
 const colors=new ColorThief().getPalette(image,6);
 if(!colors?.length) throw Error("No palette extracted");
 const p=colors[0];
 return {palette:colors.map(c=>mapColor(c,.46,.075)),
 background:mapColor(p,.23,.035),surface:mapColor(p,.34,.05),
 elevated:mapColor(p,.44,.06),accent:mapColor(p,.65,.16),tint:mapColor(p,.90,.025)};
}
```
将字符串属性写入 CSS 自定义属性，palette 写入 --palette-0 等。生产实现需评分、去重、失败回退、对比度、CORS。参考独立示例见 [Adaptive Color Demo](../examples/adaptive-color/index.html)。

## 8. 性能
取色 64×64 或 128×128；K-Means 5–8 类、10–20 次迭代；最终 3–4 色；网格 4×4/8×8；玻璃模糊 16–32px，沉浸背景 60–120px；切换 500–1000ms，流体周期 15–40s。按 URL/内容 hash 缓存，图片变化才计算；Worker/OffscreenCanvas 可选；跨域图片需 CORS。新旧背景层交叉淡入淡出，避免直接切换闪烁。移动端避免持续大半径全屏模糊。

## 9. 架构
Palette Engine（采样、聚类、评分、去重）→ Theme Engine（OKLCH、色域、深浅主题、对比度、tokens）→ Background / Glass / Components。默认采用多径向渐变，进阶使用 Mesh/WebGL。核心是感知色彩空间、低色度映射、保留空间关系。
