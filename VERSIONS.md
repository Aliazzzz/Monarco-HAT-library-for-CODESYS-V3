# Current version: 2.0.0.0
- Works as an IO driver, instead of a function block,
- All interaction are done via IO and Parameters, no function Block calls needed,
- Breaks compatibilty with v1.0.0.0 however improves greatly on ease of use.
- Supports basic features like AI, AO, DI, DO and Hardware Watchdog,
- Not yet supported: Counters, PWM, RS485.


# Previous version: 1.0.0.0
- Works as a function block, all interactions with the hardware must be done via this function block in the user program,
- Overhaul of architecture for stability and speed,
- Classic calls of function block dropped (classic IEC),
- Function block calls via OOP methods & properties (no interfaces),
- Supports basic features like AI, AO, DI, DO and Hardware Watchdog,
- Supports advanced features like Counters, PWM, RS485.
- Deprecated for v0.9.0.3.
