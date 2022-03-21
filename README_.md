# Mini Tidal Set

## The Process
- I started out with trying out different patterns in the banks and seeing what meshed well together and worked. I began the process with percussion and trying different variations of this specific pattern.
<pre>
s " ~ bd ~ ~ bd ~ ~ bd ~ ~ bd ~ ~ bd bd bd”
</pre>
- A simple yet functional pattern that alone sounds good. From there I began to build adding this pattern after having established my bass drum rhythm. I added this hand clap on top of the bass drum to help build my foundation.
<pre>
s "~ hc ~ ~ hc ~ ~ hc ~ hc ~ ~ hc”
</pre>
- From there I started trying more variations of the two patterns and even tried some of my old code that I had formulated earlier this semester. Though none of it seemed to click for me.
<pre>
s "[hh hh*3, hc bd*5] “
s " bd bd ~ bd bd bd ~ hc bd ~ hc hh”
note (scale "locrian" "0 2/2 4/3 7/4 9/5 11/6") # s “jungbass"
note (scale "locrian" "0 2/2 4/3 7/4 9/5 11/6") # s “808hc"
s "bd bd bd bd hh hc”
s "~ bottle ~ click"
s "~ hh ~ hh ~  hh ~ hh”
s "bd ~ bd*3 ~ bd bd”
</pre>
- After going through these patterns I decided to outsource and see what was available to me via the web, as I knew what I was looking for, sound wise, but was unsure how to express those ideas through the code. I ended up finding these patterns and started to alter them from a website listed below.
<pre>
n "0 1*2 2*4 <3 4>" # s "<glitch coffee>”
n "0 1*2 2*4 <2 4>" # s "<bottle>”
s "coffee glitch*8" # n (irand 39) #gain 1.5
s" birds coffee*8”
s "coffee*8" # n (irand 39) #gain 1.5
n "0 1*2 2*4 <3 4>" # s "<jungbass>" #gain 1.5
s "coffee*8" # n (irand 100) #gain 1.5
n "0 1*2 2*4 <3 4>" # s "<jungbass glitch>" #gain 1.0
</pre>
https://pdxopen.tech/courses/algomusic-ii-tidalcycles-midi-and-beyond/lessons/estuary-minitidal-finding-and-choosing-samples/

- The process started to pick up after this as I just begun to improv and alter these patterns to my liking while performing which not only provided security and stability but fluidity as well.










## SynthDef Scheduling
- Review:
  - Iterating and looping
    - Because SC is totally OOP, have to use an object method to iterate
    - **.do** is the most common
  <pre>
  10.do({ "SCRAMBLE THIS 10 TIMES".scramble.postln; })
  </pre>
  - **PBind** is a class to make Patterns with which binds values and keys together to control synths, passes that functionalty to a **Stream**
- Routines:
  - Pattern-less iteratation and looping.
  - You still need to pass information to a stream.
  - Need to sync things with clocks?
    - SystemClock: Most reliable
    - TempoClock: Best for beats
  - Need to start and stop iterations+clocks?
    - **Routine**
  - Need to start and stop iterations without clocks?
    - **Task**
<pre>
(

SynthDef(\bleep,{ arg out=0, note=60, amp=0.5, pan=0.0;

	var freq, env;

	freq = note.midicps;

	env = EnvGen.ar(

					Env([0,1,1,0],[0.01, 0.1, 0.2]),

					levelScale:amp,

					doneAction:2

				);

	Out.ar(out,

		Pan2.ar(Blip.ar(freq) * env, pan)

	)

}).add;

)
/// SystemClock
(

SystemClock.sched(0.0,//start at 0.0 sec from now, i.e. immediately

	{//a function which states what you wish to schedule

		Synth(\bleep);

		1		//repeat every second

	}

)

)
/// TempoClock
(

var t;



t = TempoClock(2); // make a new tempoclock at tempo 120 bpm = 2 beats per second



t.schedAbs(0, { arg ... args;	// start at absolute beat 0 immediately

				args.postln;	//  post the input arguments to our event function

							//  (will post logical time in beats, elapsed time

							//  in seconds of enclosing thread and this clock)



				Synth(\bleep);// make a bleep

				1.0	// reschedules every beat

})



)
/// Simple Routine
(

r = Routine({

		1.wait;

		Synth(\bleep);

		2.wait;

		Synth(\bleep);

	});

)

r.play;
r.stop;
</pre>
  - **Forks**
    - Routine shortcut. Wraps routine into .play and allows you to pass a clock into it.
<pre>
(

{16.do{arg i; Synth(\bleep, [\note,rrand(48,84) ,\amp, rrand(0.0,0.125)]); 0.125.wait} }.fork(TempoClock(2))

)
</pre>

## Samples and Buffers
- You must load audio onto the server in order to play with it
- **Buffer** is where you store that audio on the server
- **.read** loads the audio
- **b** is a global variable for buffers
- **PlayBuf** and **BuffRd** two classes to read Buffers
  - PlayBuf runs through, BuffRd lets you choose where you're playing
<pre>
(

//this loads into a buffer the default sound that comes with SuperCollider

b = Buffer.read(s,Platform.resourceDir +/+ "sounds/a11wlk01.wav");


SynthDef("playbuf",{ arg out=0,bufnum=0, rate=1, trigger=1, startPos=0, loop=1;

	Out.ar(out,

		Pan2.ar(PlayBuf.ar(1,bufnum, BufRateScale.kr(bufnum)*rate, trigger, BufFrames.ir(bufnum)*startPos, loop),0.0)

	)

}).add;

)
Synth(\playbuf, [\out, 0, \bufnum, b.bufnum]);
///
(

b = Buffer.read(s,Platform.resourceDir +/+ "sounds/a11wlk01.wav");



//using Mouse to scrub through- X position is normalised position 0 to 1 phase through the source file

SynthDef("bufrd",{ arg out=0,bufnum=0;

	Out.ar(out,

		Pan2.ar(BufRd.ar(1, bufnum, K2A.ar(BufFrames.ir(b.bufnum)*MouseX.kr(0.0,1.0)).lag(MouseY.kr(0.0,1.0))),0.0)

	)

}).play(s);

)
///all examples this week based on: https://composerprogrammer.com/teaching/supercollider/sctutorial/tutorial.html
</pre>

## Busses
  - What is a bus?
  - Everything in SC is on a bus
  - Gotta tell it which bus all the time
  - **Out** UGen controls output busses
<pre>
{ Out.ar(0, LFPulse.ar(220, 0, 0.5, 0.3)) }.play; // left speaker (bus 0)
{ Out.ar(1, LFPulse.ar(220, 0, 0.5, 0.3)) }.play; // right speaker (bus 1)
{ Out.ar(2, LFPulse.ar(220, 0, 0.5, 0.3)) }.play; // third speaker (bus 2)
</pre>
  - **Pan2** UGen most common/useful for stereo
<pre>
SynthDef("firstSynth", {Out.ar(0, SinOsc.ar(220))}).add;
a = Synth("firstSynth");
a.free;
//
SynthDef("secondSynth", {Out.ar(0, Pan2.ar(SinOsc.ar(220)))}).add;
b = Synth("secondSynth");
b.free;
</pre>

  - Advanced audio rate vs control rate
<pre>
SynthDef("thirdSynth", {Out.ar(0, Pan2.ar(SinOsc.ar(220), SinOsc.kr(2)))}).add;
c = Synth("thirdSynth");
c.free;
</pre>
  - **Splay** is also fantastic/recommended (more on this later!)
<pre>
Ndef(\u).play
Ndef(\u, {Splay.ar(Ringz.ar(Impulse.ar([1, 1.1, 1.2]), [500, 505, 550], [0.1, 0.05, 0.01]))})
Ndef(\u).gui
</pre>
  - Nodes are objects that live on busses! Not made explicitly.
<pre>
Ndef(\s).play
Ndef(\s, {SinOsc.ar([220, 440])})
Ndef(\s).gui
</pre>

## For week after next(after spring break):
- Create a Synth using the UGens
  - SynthDef
  - EnvGen
  - Pan2
- where one .kr oscillator controls an .ar oscillator
