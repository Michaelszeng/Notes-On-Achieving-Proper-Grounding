# Notes-On-Achieving-Proper-Grounding

- Energy doesn't travel thru V or I, rather through E/B-fields that propogate around traces. The current passing through traces simply induces and guides these fields, exactly like a waveguide.
  ![image](https://github.com/Michaelszeng/Notes-On-Achieving-Proper-Grounding/assets/35478698/b8861f8f-9e6a-4b40-a00c-1d5279f40021)

- Therefore, it's incorrect to think of GND as a return path in the sense that current flows from source to load then back to source via the GND plane. The return current begins as soon as the forward current begins, because the E/B-fields induced go both ways.

- The reason cross-talk and interferance exist is that the E/B-fields collide.

- KEY TO LOWERING IMPEDANCE (decreasing inductance and increasing capacitance):
  - Impendance to change in current
  - Caused by inertia of E/B-field
  - To lower inductance:
    - Keep field volume low
    - i.e. put GND plane as close as possible to signal trace (minimize the gap between forward and return paths, which is the space available for the E/B-fields
  - SUMMARY: KEEP FORWARD/RETURN PATHS CLOSE TOGETHER!
 
- In high-freq circuits (i.e. above 100 KHz), the return path (even if you have an uninterrupted GND plane, and a really squiggly forward path trace) is always directly under/as close as possible to the forward path
  - Energy takes path of lowest impedance
  - At high frequency, impedance is lower under the trace
  - Effectively all modern digital signals are high frequency (based on their rise time)
  - This is critical to know in layout where GND plane is not used; signal traces will just use the nearest other trace as the return path, causing cross-talk

- Why having solid, uninterrupted GND underneath a trace is critical to lower EMI
  - ![image](https://github.com/Michaelszeng/Notes-On-Achieving-Proper-Grounding/assets/35478698/55451eb8-68e6-417f-9771-a4dc7d59c6b6)
  - This image describes 4 possible cases of a GND plane routed underneath a microstrip trace (the black dotted rectangle)
  - Fig. 1 demonstrates a solid GND plane; Fig. 3 demonstrates a solid, uninterrupted GND beneath the trace; Fig. 2 demonstrates a single large disturbance to the GND path below the trace, and Fig. 4 demonstrates many small disturbances to the GND path below the trace.
  - Here's how the EMI of all compare:
  - ![image](https://github.com/Michaelszeng/Notes-On-Achieving-Proper-Grounding/assets/35478698/331ecb3a-7388-44fc-b96b-0f7b9ce5444c)
  - Intuition: when the return path is not clear, the E/B-fields spread everywhere attempting to find a way back toward the source
  - SUMMARY: KEEP THE GND BENEATH TRACES WIDE & INTACT.
    - Also: NEVER route traces across splits in GND plane. 20-30 db of noise --> failing your SDoC tests
