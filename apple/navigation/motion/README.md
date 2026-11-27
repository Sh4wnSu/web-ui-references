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

## Native Web implementation
Use requestAnimationFrame and integrate spring position and velocity. Retarget without resetting velocity. See local interactive lab below.

## CSS fallback
280ms cubic-bezier(.77,0,.175,1), or 420ms linear(0,.12 8%,.38 18%,.68 30%,.91 45%,1.02 60%,1.015 75%,1). These are approximations, not velocity-preserving physical springs. Use @supports and reduced-motion fallback.

## Internal resources
[Interactive lab](../../../examples/sidebar-motion/index.html) · [JSON presets](../../../design-tokens/spring.json) · [CSS approximations](../../../design-tokens/spring.css)
