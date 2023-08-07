# Notes-On-Achieving-Proper-Grounding

- Energy doesn't travel thru V or I, rather through E/B-fields that propogate around traces. The current passing through traces simply induces and guides these fields, exactly like a waveguide.
  ![image](https://github.com/Michaelszeng/Notes-On-Achieving-Proper-Grounding/assets/35478698/b8861f8f-9e6a-4b40-a00c-1d5279f40021)

- Therefore, it's incorrect to think of GND as a return path in the sense that current flows from source to load then back to source via the GND plane. The return current begins as soon as the forward current begins, because the E/B-fields induced go both ways.

- The reason cross-talk and interferance exist is that the E/B-fields collide.

- KEY TO LOWERING IMPEDNACE (decreasing inductance and increasing capacitance)
  - impendance to change in current
  - caused by inertia of E/B-field
  - To lower inductance:
    - Keep field volume low
    - i.e. put GND plane as close as possible to signal trace (minimize the gap between forward and return paths, which is the space available for the E/B-fields
  - SUMMARY: KEEP FORWARD/RETURN PATHS CLOSE TOGETHER!
 
- 
