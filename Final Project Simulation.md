# Final Project

## The Process
- Similar to my mini tidal set, I used the same code for my final project and expanded upon it in terms of how it is used and now use the code more intentionally with a bit more structure to ensure that certain moment to show off specific sounds will come about

core code
<pre>
s " ~ bd ~ ~ bd ~ ~ bd ~ ~ bd ~ ~ bd bd bd”
s "~ hc ~ ~ hc ~ ~ hc ~ hc ~ ~ hc”  eh
n "0 1*2 2*4 <3 4>" # s "<glitch coffee>" #gain 1.3
n "0 1*2 2*4 <2 4>" # s "<bottle>”
s "birds coffee*8"
</pre>

Everything else was added sprodically throughout the perofmrance pieces giving me this full piece with different elements, pieces of code, at hand
<pre>
n "0 1*2 2*4 <3 4>" # s "<glitch coffee>" #gain 1.3!!!

n "0 1*2 2*4 <2 4>" # s "<bottle>” !!!

s "coffee glitch*8" # n (irand 39) #gain 1.5

s "birds coffee*8” !!

s "coffee*8" # n (irand 39) #gain 1.5 !!!
s "coffee*8" # n (irand 100) #gain 1.5

n "0 1*2 2*4 <3 4>" # s "<jungbass>" #gain 1.5
n "0 1*2 2*4 <3 4>" # s "<jungbass glitch>" #gain 1.0

</pre>

# From my last documentation piece to have as a reference
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

## Maya's Part

- I am happy with the way the live / final performance turned out. I feel this was one of my favorite classes this semester and I'm glad that I've been able to learn and contrbute. A project I enjoyed naviagating and now have a set in my pocket should I chose to do a live coding performance anytime in the near future.
- although Maya and I weren't able to perform together, there was still code Maya had created for the performance!!
<pre>
## Option 1
Base code:
```
osc(5, 0.2, 0.001)
.kaleid([3,4,5,7,8,9], 0.5)
.color(0.3, 0.1)
.colorama(0.4)
.modulate(o0, 0.9)
.scale(0.3)
.out(o0)
```

To make it more crazy, change the oscillator rate:
```
osc(5, 0.9, 0.001)
```

To slowly rotate the pieces, add `.rotate`:
```
.rotate(10, 0.1)
```

Slowly change the second color value by `0.01`:
```
.color(0.3, 0.2) // first
.color(0.3, 0.3) // second
.color(0.3, 0.4) // third
```
## Option 2
Base code:
```
noise(3,0.1,7)
.rotate(1,-1,-2).mask(shape(20))
.colorama(0.5)
.modulateScale(o0)
.modulateScale(o0,1,)
.blend(o0)
.blend(o0)
.blend(o0)
.blend(o0)
.out(o0)
```

```
noise(3,0.6,2)
.rotate(1,-1,-20)
.colorama(5)
.blend(o0)
.blend(o0)
.luma(0.1, 1)
.out(o0)
```

Add `.luma(0.1, 1)` to darken
<pre>
