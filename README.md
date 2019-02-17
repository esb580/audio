# audio
#Berringer/Jack/Guitarix/Audacity Setup on Ubuntu 18.04

#Description: 

This documents my working Linux DAW, because it was not easy to figure out. In fact it was painfully hard to figure out even with the easiest apps available for doing amp and pedal sampling along with recording.  

#Hardware:
- Dell T3500 12GB RAM, SATA Drive, 4 Core x 2 Thread Intel Xeon
- Berringer UM2 USB Audio Interface plugged into USB 2 Port
  - Instrument Gain Knob Dimed
  - Output Knob at 2:00
- Edifier Studio Monitors connected to Berringer with stereo cable
- Electric Guitar physically jacked into Berringer Instrument Port

#Main Packages added:
- Audacity - Pretty "simple", verging on intuitive. Good docs and userbase. Nice results on playback. 
- Guitarix - Was able to get a clean sound without too much tweaking, and add virtual representations of pedals I am familiar with. GUI makes it pretty nice to figure out what you are doing on a virtual level, and the controls are easy to understand. 
- Jack/qjackctl - Needed some mental leaps to get going, but then it was mainly a game of follow the signal path.  I guess it is as simple as it can be, but still requires a lot of up front research.  

#Other Packages tried:
- Rakarrack - The presets work OK, but my brain still needs a physical representation of what is going on.  That works better in Guitarix. Will explore more later. 
- Ardour 5 - For recording.  Extremely complicated to jump into and the documentation is a bit scanty.  Again, too difficult for me to understand at a beginner level.  

 
#Setup:

Providing a picture of critical settings to start with.  Will add explaination later.  

Application Startup Sequence appears to be an important issue.  

- Start up qjackctl 
   - Pop open Settings and verify  
     - Interface: hw:CODEC,0
     - Sample Rate: 44100
     - Frames/Period: Type in 147, Don't use drop down. *Document referenced.
     - Periods/Buffer: 3
   - Open the Connections - This shows how you are patched through the various inputs and outputs of your applications and system. 
   - Click Start
      - You should now see "System" in Jack Connections

- Start up Guitarix
   - Make the same connections shown in my picture between gx_head_amp, gx_head_fx, and system.
   - You should be able to play through the amp at this point. 

- Open Audacity
   - Take Picture to show defaults in case it gets screwed up.
   - Change your signal path from defaults to: (Reference Picture)
     - Audio Host: JACK Audio Connection Kit
     - Recording Device: gx_head_fx
     - Recording Channel: 1(Mono) Recording Channel
     - Playback Device: System
    


