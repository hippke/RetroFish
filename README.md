# RetroFish

RetroFish is based on [Stockfish](https://stockfishchess.org), the strongest chess engine. It aims to port the most recent version to the oldest possible machine, including the NNUE evaluation based on efficiently updatable neural networks.

![image](https://raw.githubusercontent.com/hippke/RetroFish/master/docs/logo.png)

## Why run Stockfish on very old computers?
My key motivation is an impossible question: Would the artificial general intelligence of the future run on present hardware? Would it run on even older hardware? Perhaps all we need for real machine intelligence is the right algorithm? This problem is also known as "hardware overhang". (Some of my thoughts: [1](https://www.lesswrong.com/posts/75dnjiD8kv2khe9eQ/measuring-hardware-overhang), [2](https://www.lesswrong.com/posts/75dnjiD8kv2khe9eQ/measuring-hardware-overhang), [3](https://www.lesswrong.com/posts/J6gktpSgYoyq5q3Au/benchmarking-an-old-chess-engine-on-new-hardware)).

There is a way to gather some insight regarding these questions. We can take modern AI algorithms, port them backwards as much as possible, and examine the effects. As usual, making real experiments is most useful. 

## Chess engine background

In 1997, the IBM supercomputer "Deep Blue" defeated the world chess champion, Gary Kasparov. The same was possible for chess engines running on standard computers about a decade later. Modern algorithms like Stockfish can beat any human player, even when running on mobile phones. Let us take the best engine of today, and run it on old hardware. Does that even work? How strong will it be?

## How far back can we go?
To make this experiment somewhat realistic, I will stick to standard hardware and skip over exotic supercomputers. Inside this scope, there are several limitations to consider. 

### RAM
Stockfish 14 uses a neural network with a size of 45 MB, plus a few MB for the engine, plus some hash for the search tree. In addition, we want to run an operating system and a way to transmit the best moves (e.g., an SSH session). I find that 64 MB are sufficient with swapping (reducing performance), and 128 MB should be fine. This requirement immediately excludes PCs from the 386 era and older, except perhaps exotic server hardware or MIPS/RISC hardware. I may look into these at a later time. The following generation of 486 CPUs, however, provides several consumer class mainboards which support 256 MB of RAM. Back in the days, a configuration with 4 or 8 MB was typical. In 1990, a set of 256 MB of RAM chips would have cost the equivalent of a nice car. Today, we can buy the hardware on a flea market (and hope it still runs).

### Compilation
Can we run Stockfish on a 486 with a lot of RAM? Yes, we can! It is not trivial, but most of the compexity is in the foundation. Stockfish is open source, so we can modify and compile it. There are two main options: Windows and Linux. Due to my familarity with the latter, I chose Linux. Building on [this great tutorial](https://github.com/yeokm1/gentoo-on-486), I managed to install Gentoo Linux with the most recent Kernel 5.10 on a 486 machine. Here is a screenshot of the installation from a VM:

![image](https://raw.githubusercontent.com/hippke/RetroFish/master/docs/qemu.png)

Using a recent software stack is very useful, because SF14 requires a C++-17 compiler to build (there is also the [CFish port](https://github.com/syzygy1/Cfish) which only requires C-11). Using GCC-10 or GCC-11, we can build Stockfish on the 486 with some Makefile modifications.

### Real retro hardware!?
Yes, I plan to run this on a real 486 DX2-66 MHz manufactured in 1992. I can also be run on a 486 DX-33 MHz from 1989 at half speed. I plan to add a Youtube video of the system in action. 

Why not just use a VM?
- For the fun of it!
- As a real benchmark: It is very difficult to adjust RAM latency etc. in a VM. To really determine the speed, let's use real hardware from around 1990 :-)


## How strong is RetroFish?
On a 486DX2-66 MHz, it calculates about X kNodes per second. Under standard time control (about 3 minutes per move), it calculates X kNodes per move. Following my ELO-with-nodes estimate, its strength should be in the XXXX ELO range under tournament conditions. 

## Can I play against RetroFish without powering up my old 486 PC?

Yes, soon! I plan to provide a [Lichess bot](https://lichess.org/player/bots) against which you can play for free. Good luck!

