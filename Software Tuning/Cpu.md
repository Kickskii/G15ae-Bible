# Introduction
Silicon lottery

## BIOS side
- explain the entirety of PBO and what everything is and how it works
- how to figure out motherboard PBO limits
- how to test reducing different pbo limits and their effect on performance
- finding a golden middle point
- how changing the boost frequency in PBO can affect latency slightly
## OS side
- setting power limits in Ghelper before starting #g15_specific
- PBO limits part 1 [-5 test]
- explain why the -5 test exists
- revamp the -5 test to include p95 SSE 60m per core as well as y cruncher for 40m per core
- explain why we stress test and why this is EXTREMELY important to do
- if they passed the -5 test 
- PBO limits part 2 

## Introduction to Curve Optimizer 
why is it not exactly undervolting
why PerCore and why not just use AllCore
the two methods of doing per core and why to use one over the other
what is the lookup table
glancing over the formula to calculate the lookup table
easier way to interpret the lookup table
what cpus can the lookup table work on
what needs testing (dual ccd's)
what the tools ie Y cruncher and P95 are and why do we use them
what are the different modes for these in core cycler and how they are differernt and why do we gotta do such long tests using them
what are we going to do with the ryzenadj script
link to ryzenadj documentation and link to isle of zen discord in case you want to know about more commands
how to use premade RyzenAdj script to do percore for every core one by one
going from high to low this time 
explaining the corecycler config file and how jank my setup for it is
what error look like
why errors are bad
what running unstable will do
having a final test involving 6 iterations of Y cruncher on every core as well as 2 hours of Prime95 on each core

after finishing noting down all performance metrics in the excel sheet/notepad/mobile notes app by doing CPU benchmarks

## Considerations
setting up Task Scheduler and setting it to disabled so as to enable it back up after RAM tuning
	 I believe per core can be used in the bios
	