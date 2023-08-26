# Checklist on what needs to be explained
## like a guideline of a script idk 

Intro
there are timestamps on the video and a extensive checklist in the discription about everything feel free to jump around
join the discord

checking the ram
getting an external display cable
getting new ram + ram recommendations 

checking the performance OOTB
some stock performance numbers with good stock ram
>>should we do ram tuning as the opening?
>>could technically just tell about it during the ram section if needed

Disclaimer about damage to your machine being at their own risk we just sharing the findings and methords we the g15ae community found
preach about stability and proper testing 

Disclaimer about performance gain being based on silicon lottery
steps to do before starting
downloading my redone toolbox ((the toolbox is shit please redo it))
reinstalling windows (can be using ReviOS or whatever(example GhostSpectre or Tiny11))
installing Drivers using the toolbox
not having asus shitty bloatware
deleting the dll's from ghelper 

-Disclaimer about AMD Adrenaline Drivers(mention installation of Custom Amernimez Drivers in the GPU section)  (ppt tables being locked after 23.3.2)
-making an excel gathering baselines and noting down performance numbers as well as core clocks
-maybe use CPU Z for baselines for before and after Curve Optimiser single core testing
-show how to disable windows telemetry and driver updates from windows update
disable firmware device to completely block bios updates

Bios Recommendation + why 316 and in which case its fine to use latest(iets)
explaining differences between the bios versions as per personal findings

setting up the Flash drive/SSD for UMAF Bios Editor as well as the Optional downgrade
show how to downgrade the bios
explaining what just happened and what we about to do when we jump into UMAF for the first time
explain the entirety of PBO and what everything is and how it works
how to test different pbo limits and their effect on performance

setting power limits in Ghelper before starting
PBO limits part 1 -5 test
explain why the -5 test exists
revamp the -5 test to include p95 SSE 60m per core as well as y cruncher for 40m per core
explain why we stress test and why this is EXTREMELY important to do
if they passed the -5 test 
PBO limits part 2 g15 ae specific

Introduction to Curve Optimizer
why is it not exactly undervolting
why PerCore and why not just use AllCore
the two methods of doing per core and pro's and cons of them
how to use premade RyzenAdj scripts to do percore for every core one by one
going from high to low this time cause time is of the essence
what error look like
why errors are bad
what the tools ie Y cruncher and P95 are and why do we use them
having a final test involving 6 iterations of Y cruncher on every core as well as 2 hours of Prime95 on each core

after finishing noting down all performance metrics in the excel sheet/notepad/mobile notes app by doing CPU benchmarks

setting up Task Scheduler and setting it to disabled so as to enable it back up after RAM tuning

WELCOME TO HELL

*insert ram tuning shit in here*
;-;
uhhhh [[ram tuning]]




GPU TUNING
*this is pretty chill im about to make it not chill*

what is hybrid mode vs dGPU mode and why it affects performance
how to reduce the performance penalty on hybrid mode


amd cleanup utility vs DDU
official download area and how to install official drivers
MPT on official drivers
whats still possible with tests
amernime drivers
which one to use
what is flex arch and why am i not using it
tweaks i use
finishing up with setup and getting a different ui
OCD about taskbar icon but its fine
sidenote about gpu now being called something more interesting

take a backup from GPU Z

load it in Morepowertools
click the drop down box and select dGPU
what is what and what even works 
do not mess with feature control unless you know what you're doing
whats the OC limits for and how they might not matter
Vmin/Vmax 
how power limit input does nothing and something at the same time
what TDC limits are 
what is ULV stuff
what is VDDCI and what you can do with it 
whats temprature dependent vmin 
whats in the frequency tab
what are gfx clocks
what is soc clock
what are vclk dclk dcefclk dispclk pixclk phyclk dtbclk and fclk ,boost fclk
how fclk might be locked in vbios and why we still set it higher
whats staticvoltageoffset
what is linear droop
what are DcBtc and DcTol
why fan tab is irrelevant
why not to mess around in the more tab
briefly glance over the parameters on the more curve section
how to tune your gpu
a few starter MPT profiles i have for you to use or mess around with

moreclocktool: why you dont exactly need adrenaline software but have it anyways
what you should and shouldnt change
what happens when you change something and your clock is locked to minimum

freesync 
how to turn it on without using amd software //research needed

monitor resolution for benchmarking and why should you care
monitor refresh for benchmarking and why should you still care
how lower than 1080p for monitor resolution doesnt give you more score

benchmarking 

how to get icc profile for your laptop panel
