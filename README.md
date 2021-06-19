Performance of standard (**monolithic CUDA**) vs topologically-ordered components
(**levelwise CUDA**) PageRank ([pull], [CSR], [skip-teleport], [compute-5M]).

This experiment was for comparing performance between:
1. Find **CUDA** based pagerank with standard algorithm (**monolithic**).
2. Find **CUDA** based pagerank in topologically-ordered components fashion (**levelwise**).

Both approaches were attempted on different types of graphs, running each
approach 5 times per graph to get a good time measure. **Levelwise** pagerank
is the [STIC-D algorithm], without **ICD** optimizations (using single-thread).
On average, **levelwise** pagerank is **same** performance as the *monolithic*
approach.

All outputs are saved in [out](out/) and a small part of the output is listed
here. All [charts] are also included below, generated from [sheets]. The input
data used for this experiment is available at ["graphs"] (for small ones), and
the [SuiteSparse Matrix Collection].

<br>

```bash
$ g++ -O3 main.cxx
$ ./a.out ~/data/min-1DeadEnd.mtx
$ ./a.out ~/data/min-2SCC.mtx
$ ...

# ...
#
# Loading graph /home/subhajit/data/web-Stanford.mtx ...
# order: 281903 size: 2312497 {}
# order: 281903 size: 2312669 {} (loopDeadEnds)
# order: 281903 size: 2312669 {} (transposeWithDegree)
# [00012.078 ms; 000 iters.] [0.0000e+00 err.] pagerankNvgraph
# [00010.097 ms; 063 iters.] [7.0437e-07 err.] pagerankMonolithic
# [00009.169 ms; 063 iters.] [7.0437e-07 err.] pagerankLevelwise
#
# ...
#
# Loading graph /home/subhajit/data/soc-LiveJournal1.mtx ...
# order: 4847571 size: 68993773 {}
# order: 4847571 size: 69532892 {} (loopDeadEnds)
# order: 4847571 size: 69532892 {} (transposeWithDegree)
# [00165.932 ms; 000 iters.] [0.0000e+00 err.] pagerankNvgraph
# [00177.466 ms; 058 iters.] [2.6097e-06 err.] pagerankMonolithic
# [00169.848 ms; 058 iters.] [2.6097e-06 err.] pagerankLevelwise
#
# ...
```

[![](https://i.imgur.com/2K0WuWu.gif)][sheets]
[![](https://i.imgur.com/wn0Od0x.gif)][sheets]

<br>
<br>


## References

- [STIC-D: algorithmic techniques for efficient parallel pagerank computation on real-world graphs][STIC-D algorithm]
- [PageRank Algorithm, Mining massive Datasets (CS246), Stanford University](http://snap.stanford.edu/class/cs246-videos-2019/lec9_190205-cs246-720.mp4)
- [SuiteSparse Matrix Collection]

<br>
<br>

[![](https://i.imgur.com/uF80zAS.jpg)](https://www.youtube.com/watch?v=riC9mRFp1ig)

[SuiteSparse Matrix Collection]: https://suitesparse-collection-website.herokuapp.com
[STIC-D algorithm]: https://www.slideshare.net/SubhajitSahu/sticd-algorithmic-techniques-for-efficient-parallel-pagerank-computation-on-realworld-graphs
["graphs"]: https://github.com/puzzlef/graphs
[pull]: https://github.com/puzzlef/pagerank-push-vs-pull
[CSR]: https://github.com/puzzlef/pagerank-class-vs-csr
[skip-teleport]: https://github.com/puzzlef/pagerank-levelwise-skip-teleport
[compute-5M]: https://github.com/puzzlef/pagerank-levelwise-cuda-adjust-compute-size
[charts]: https://photos.app.goo.gl/xeZWBbSgBcCMDhDBA
[sheets]: https://docs.google.com/spreadsheets/d/1OMmcMTKi9TYyhyZBZjP9c7sceMAapPbyn-GW0gngn9k/edit?usp=sharing
