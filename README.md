# audio
# Behringer UM2/Jack/Guitarix/Audacity Setup on Ubuntu 18.04

# Description: 

This documents my working Linux DAW, because it was not easy to figure out. In fact, it was painfully hard to figure out even with the easiest apps. My goal is doing amp and pedal sampling along with recording on my favorite at-home distro. I used Ubuntu Studio previously and received similar results on a laptop, but did not document.  So, this time, I am not making that mistake.   

# Hardware Used:
- Dell T3500 12GB RAM, SATA Drive, 4 core x 2 thread Intel Xeon X5687 @ 3.60GHz
- Behringer U-Phoria UM2 USB Audio Interface plugged into USB 2.0 port
  - Instrument Gain Knob Dimed
  - Output Knob at 2:00
  - Edifier speakers connected to Behringer rear ports with stereo cable 
  - Electric Guitar physically jacked into Behringer front/middle Instrument Port
- Note: My resources are not impacted by this setup hardly at all. So, I assume a smaller workstation would be fine, too.

# Main Packages added:
1. Audacity - Pretty "...simple", verging on intuitive. Good docs and user base. Nice results on playback. 
2. Guitarix - Was able to get a clean sound without too much tweaking, and add virtual representations of pedals I am familiar with. GUI makes it pretty nice to figure out what you are doing on a virtual level, and the controls are easy to understand. One exception is the knob controls are funky and take a little practice.  
3. Jack/qjackctl - Needed some mental leaps to get going, but then it was mainly a game of follow the signal path.  I guess it is as simple as it can be, but still requires a lot of up front research.  

# Other Packages tried:
1. Rakarrack - The presets work OK, but my brain still needs a physical representation of what is going on. Guitarix is better for that. Will explore rakarrack more later. 
2. Ardour 5 - For recording.  Extremely complicated to jump into and the documentation is a bit scanty.  Again, too difficult for me to understand at the moment coming from beginner level.  

 
# Setup:

Providing a picture of critical settings to start with.  Will add explanation later.  
![alt text](https://github.com/esb580/audio/blob/master/audio-daw-linux-settings.jpg)

Application Startup Sequence appears to be an important issue.  

- Start up qjackctl 
  - Take Picture to show defaults, in case it gets screwed up...(from experience)
  - Pop open Settings and verify  
    - Interface: hw:CODEC,0
    - Sample Rate: 44100
    - Frames/Period: Type in 147, Don't use drop down. *Document referenced*
    - Periods/Buffer: 3
  - Open the Connections - This shows how you are patched through the various inputs and outputs of your applications and system. 
    - Note that your Instrument Port on Behringer Maps to capture_2, while capture_1 = Microphone Port
  - Click Start
    - You should now see "System" in Jack Connections

- Start up Guitarix
  - Take Picture to show defaults in case it gets screwed up.
  - Make the same connections shown in my picture between gx_head_amp, gx_head_fx, and system.
  - You should be able to play through the amp at this point. 

- Open Audacity
  - Take Picture to show defaults in case it gets screwed up.
  - Change your signal path from defaults to: (Reference Picture)
    - Audio Host: JACK Audio Connection Kit
    - Recording Device: gx_head_fx
    - Recording Channel: 1(Mono) Recording Channel
    - Playback Device: System
  - On the audacity Recording Level control, click "Start Monitoring"
    - You should see in the Connections of qjackctl, a new Writable Client/Input Port called PortAudio
    - I did not have to make a connection for this, as it automagically connected up to out_0 on gx_head_fx. This thankfully worked out just right, unlike a lot of other stuff.  
  - At this point you can add a mono track, click record, and start rocking.  
    
- TODO: Add detailed MOP for recording process, and notes from more extensive testing.   
    
- Reference Documents:
  - https://wiki.linuxaudio.org/wiki/list_of_jack_frame_period_settings_ideal_for_usb_interface
    - A list of settings that work in qjackctl. Go to bottom of list where it talks about USB settings that "might" work.  So, far my best results are from there.
