# version: 2.0.0.1
- See version 2.0.0.0 plus
   - Added Hardware Watchdog 
   - Added Control Byte
- Stable, but work in progress ...
 

# version: 2.0.0.0
- Implemented as CODESYS 3 IO device-driver;
   - 100% Open source,
   - 100% Pure IEC code (ST).
- No function block calls in your software necessary, just write code, attach variable to an I/O channel, ready! 
- Breaks compatibilty with earlier FB version but improves highly on ease of use,
   - 4 Di,
   - 4 Do,
   - 2 Ai,
   - 2 Ao,
 - Stable, but work in progress ...


# version: 1.0.0.0
- Works as a function block, all interactions with the hardware must be done via this function block in the user program,
- Overhaul of architecture for stability and speed,
- Classic calls of function block dropped (classic IEC),
- Function block calls via OOP methods & properties (no interfaces),
- Supports basic features like AI, AO, DI, DO and Hardware Watchdog,
- Supports advanced features like Counters, PWM, RS485.
- Deprecated for v0.9.0.3.
