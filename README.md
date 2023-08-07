# Notes-On-Achieving-Proper-Grounding

https://www.youtube.com/watch?v=ySuUZEjARPY

This video is freaking blowing my mind.

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
   
  - Case Study:
    - This PCB was emitting tons of EMI + not working.
    - ![image](https://github.com/Michaelszeng/Notes-On-Achieving-Proper-Grounding/assets/35478698/42ed3d25-6915-4091-be4c-6428265a57d0)
    - Notice: traces crossing vertically and horizontally on adjacent layers
      - These is is like routing across a massive split in the GND plane
      - Traces in each layer were trying to use each other as return paths --> cross-talk
    - SOLUTION: if you MUST route traces like this on adjacent layers, put GND traces (shown in white) between the adjacent signal traces on both layers
      - ![image](https://github.com/Michaelszeng/Notes-On-Achieving-Proper-Grounding/assets/35478698/a151a9ba-3b61-4cf6-8a61-e78bd81ff5fa)
      - This way, signals will use the GND traces for return path --> performed way better
     
- Caution for 4-layer boards:
  - Typical Stackup (note the spacing btwn layer 2, 3):
  - ![image](https://github.com/Michaelszeng/Notes-On-Achieving-Proper-Grounding/assets/35478698/519117ad-1dd7-4b04-9135-5b1e907dd1a5)
  - Both signals on layer 1 and 2 try to use layer 3 as return path:
  - ![image](https://github.com/Michaelszeng/Notes-On-Achieving-Proper-Grounding/assets/35478698/999fd993-729a-4ddd-ba8a-6d7a48270500)
  - Signals on layer 1 and 2 that cross over each other --> E/B-fields couple --> severe EMI (not a signal integrity problem though)
  - SOLUTION: Route signals on layer 1 as triplets (GND traces between pairs of signal traces; see above)

- Note: PWR (instead of GND) can also be used as return path for a signal IF PWR plane/trace is identical to the source driving the signal
  - Best for the PWR plane/trace that is the return path to be on the same layer (no explanation provided)

- When moving energy between layers, route on either side of same GND plane
  - This way, E/B-fields stay around the same plane, don't spread --> no interferance/EMI
  - If not possible, put a GND via(s) very nearby. GND via will help guide/contain the E/B-fields (will remain between the signal and GND via)

- Component placement
  - Analog in 1 area, digital in another
  - Keep different operating voltages in different places
  - For inter-board conns, put conns as close to IC as possible (or noise will go into next board + wires will act as antennas --> EMI failure)
  - Avoid routing traces of different voltage/type in an area

## PRACTICAL TAKE-AWAYS:
- Route signals with respect to GND (or PWR) like you actually mean it (have a low-impedance GND nearby)
- Use GND plane if possible
- If EMI is a concern, be extremely cautious of signals on different layers crossing over each other. See above for solutions to this problem.
- 
