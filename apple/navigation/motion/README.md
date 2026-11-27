# Apple-inspired Spring Motion

Apple SwiftUI provides smooth, snappy and bouncy spring presets. The following Web presets are independent approximations, not Apple's internal parameters.

## Physics
m x'' + c x' + k(x-target)=0. Damping ratio ζ=c/(2√(km)). ζ<1 underdamped (overshoot), ζ=1 critically damped, ζ>1 overdamped. Preserve position and velocity when retargeting; settle when both displacement and velocity are below thresholds.
|Preset|Stiffness|Damping|Mass|ζ|
|---|---:|---:|---:|---:|
|smooth|300|35|1|1.01|
|professional|380|38|1|0.97|
|snappy|450|34|1|0.80|
|soft|220|27|1|0.91|
|bouncy|300|16|1|0.46|

## Sidebar choreography
240 → 60px; high-damping Professional or Smooth; visual target 280–350ms (actual settling depends on physics). Main content follows width; icons remain fixed. Text exits 100–140ms immediately; enters after 120–150ms with 140ms fade, blur 2→0px and translation 4→0px. Submenu stagger 20–33ms; selection highlight spring 500/40/1. Avoid excessive bounce in frequently used navigation. Preserve focus, prevent clipping and wrapping, support reduced motion, no initial animation. Save user preference separately if needed.

## React Motion
```tsx
import {motion,useReducedMotion} from "motion/react";
function Sidebar({collapsed,children}) {
 const reduce=useReducedMotion();
 return <motion.aside initial={false} animate={{width:collapsed?60:240}}
 transition={reduce?{duration:0}:{type:"spring",stiffness:380,damping:38,mass:1}}
 style={{flexShrink:0,overflow:"hidden"}}>{children}</motion.aside>;
}
```
Alternative: {type:"spring",visualDuration:.28,bounce:.08}. For layout changes use layout and layout="position" for text to avoid scale distortion. Width animation triggers layout; profile dense dashboards.

## CSS fallback
280ms cubic-bezier(.77,0,.175,1), or 420ms linear(0,.12 8%,.38 18%,.68 30%,.91 45%,1.02 60%,1.015 75%,1). These are approximations, not velocity-preserving physical springs. Use @supports and reduced-motion fallback.

## References
- [Apple Animate with springs](https://developer.apple.com/videos/play/wwdc2023/10158/)
- [SwiftUI Animation](https://developer.apple.com/documentation/swiftui/animation)
- [HIG Motion](https://developer.apple.com/design/human-interface-guidelines/motion)
- [Animate UI Sidebar](https://animate-ui.com/docs/primitives/react-aria/sidebar) — choreography reference.
- [Aceternity Sidebar](https://ui.aceternity.com/components/sidebar)
- [Motion spring](https://motion.dev/docs/react-transitions), [Layout](https://motion.dev/docs/react-layout-animations), [source](https://github.com/motiondivision/motion)
- [React Spring](https://www.react-spring.dev/), [GSAP Flip](https://gsap.com/docs/v3/Plugins/Flip/), [AutoAnimate](https://github.com/formkit/auto-animate), [easings](https://easings.net/).
Upstream links are reference entrances, not vendored code; versions/licenses not individually verified.

[Interactive lab](../../../examples/sidebar-motion/index.html) · [JSON presets](../../../design-tokens/spring.json) · [CSS approximations](../../../design-tokens/spring.css)
