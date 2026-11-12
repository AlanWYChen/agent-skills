---
name: performance
description: "Guide mobile performance. Use when implementing or reviewing runtime performance, responsiveness, resource usage, and bottlenecks in mobile applications."
---

# Mobile Performance

Track:
- startup time
- time to interactive
- dropped frames/jank
- memory
- battery
- network usage
- disk usage
- crash-free sessions

Measure on representative devices with platform tooling (Xcode Instruments, XCTest metrics, Android Macrobenchmark/Profiler) and establish a baseline before optimizing.

Define cold/warm/hot start and a frame budget (16.7 ms at 60 Hz, 8.3 ms at 120 Hz), plus app size budgets with App Bundle splits and on-demand delivery where relevant.

Consider:
- lazy initialization
- image resizing/caching
- list virtualization
- avoiding work on main/UI thread
- background work limits
- offline caching
- pagination
- efficient serialization
- minimizing unnecessary bridge/native-module calls in hybrid stacks
