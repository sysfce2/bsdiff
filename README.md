# Binary diff/patch utility
**bsdiff** and **bspatch** are tools for building and applying patches to binary files.</br>
By using suffix sorting (specifically, [Larsson and Sadakane's qsufsort](http://www.cs.lth.se/Research/Algorithms/Papers/jesper5.ps)) and taking advantage of how executable files change, **bsdiff** routinely produces binary patches 50-80% smaller than those produced by [Xdelta](http://sourceforge.net/projects/xdelta/), and 15% smaller than those produced by [.RTPatch](http://www.pocketsoft.com/products.html) (a $2750/seat commercial patch tool).

These programs were originally named **bdiff** and **bpatch**, but the large number of other programs using those names lead to confusion; I'm not sure if the "bs" in refers to "binary software" (because **bsdiff** produces exceptionally small patches for executable files) or "bytewise subtraction" (which is the key to how well it performs).</br>
Feel free to offer other suggestions.

**bsdiff** and **bspatch** use bzip2; by default they assume it is in /usr/bin.

**bsdiff** is quite memory-hungry. It requires <i>max(17</i>\*<i>n,9</i>\*<i>n+m)</i>+<i>O(1)</i> bytes of memory, where <i>n</i> is the size of the old file and <i>m</i> is the size of the new file.</br>
**bspatch** requires <i>n</i>+<i>m</i>+<i>O(1)</i> bytes.

**bsdiff** runs in <i>O((n</i>+<i>m) log n)</i> time; on a 200MHz Pentium Pro, building a binary patch for a 4MB file takes about 90 seconds.</br>
**bspatch** runs in <i>O(n</i>+<i>m)</i> time; on the same machine, applying that patch takes about two seconds.

Providing that <i>off_t</i> is defined properly, **bsdiff** and **bspatch** support files of up to 2^61-1 = 2Ei-1 bytes.

The algorithm used by BSDiff 4 is described in my (unpublished) paper [Naive differences of executable code](http://www.daemonology.net/papers/bsdiff.pdf); please cite this in papers as

<blockquote>Colin Percival, <i>Naive differences of executable code</i>, <tt>http://www.daemonology.net/bsdiff/</tt>, 2003.</blockquote>

A far more sophisticated algorithm, which typically provides roughly 20% smaller patches, is described in my [doctoral thesis](http://www.daemonology.net/papers/thesis.pdf).
