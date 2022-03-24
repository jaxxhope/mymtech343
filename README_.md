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
</pre>
- the patterns work and "alternate each cycle which represent which family os samples it's using." The # s "<glitch coffee>" tells it which family to use
<pre>
s "coffee glitch*8" # n (irand 39) #gain 1.5
</pre>
this patterns chooses a randomly chooses a different sample out of the family every beat.
<pre>
s" birds coffee*8”
s "coffee*8" # n (irand 39) #gain 1.5
n "0 1*2 2*4 <3 4>" # s "<jungbass>" #gain 1.5
s "coffee*8" # n (irand 100) #gain 1.5
n "0 1*2 2*4 <3 4>" # s "<jungbass glitch>" #gain 1.0
</pre>
- After slightly altering, these were some of the patterns I was left with
https://pdxopen.tech/courses/algomusic-ii-tidalcycles-midi-and-beyond/lessons/estuary-minitidal-finding-and-choosing-samples/

- The process started to pick up after this as I just begun to improv and alter these patterns to my liking while performing which not only provided security and stability but fluidity as well.

- The only issue I ran into with this project was slight distortion in volume, which is something that could be fixed by adjusting the gain on each instrument while performing, though I didn't really mind the distortion. I enjoyed this process and loved how my comfortably has grown performing with live coding. 
