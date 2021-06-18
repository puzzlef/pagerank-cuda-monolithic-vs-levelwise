Comparing various min. component sizes for topologically-ordered components
(levelwise) [CUDA] based PageRank ([pull], [CSR]).


For this experiment **min. component size** was varied from `1E+2` - `1E+7`.
Each **min. component size** was attempted on different types of graphs,
running each size 5 times per graph to get a good time measure. **Levelwise**
pagerank is the [STIC-D algorithm], without **ICD** optimizations (using
single-thread). It appears choosing the largest **min. component size**
is the best, but that would not be useful. So, for the time being,
**min. component size** is `50000` is chosen.

All outputs are saved in [out/](out/) and a small part of the output is listed
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
# [00011.294 ms; 000 iters.] [0.0000e+00 err.] pagerankNvgraph
# [00010.037 ms; 063 iters.] [7.0437e-07 err.] pagerankMonolithic
# [00955.617 ms; 065 iters.] [5.1496e-06 err.] pagerankLevelwise [1e+02 min-component-size]
# [00324.125 ms; 062 iters.] [4.2335e-06 err.] pagerankLevelwise [5e+02 min-component-size]
# [00196.761 ms; 067 iters.] [5.5364e-06 err.] pagerankLevelwise [1e+03 min-component-size]
# [00070.219 ms; 068 iters.] [5.4311e-06 err.] pagerankLevelwise [5e+03 min-component-size]
# [00031.119 ms; 069 iters.] [4.9487e-06 err.] pagerankLevelwise [1e+04 min-component-size]
# [00015.097 ms; 070 iters.] [4.3619e-06 err.] pagerankLevelwise [5e+04 min-component-size]
# [00010.457 ms; 064 iters.] [1.9684e-06 err.] pagerankLevelwise [1e+05 min-component-size]
#
# ...
```

<br>

[![](https://i.imgur.com/kohs9Ov.png)][sheets]
[![](https://i.imgur.com/eHwowMX.png)][sheets]
[![](https://i.imgur.com/PjrAfeK.png)][sheets]
[![](https://i.imgur.com/8bZtchZ.png)][sheets]

<br>
<br>


## References

- [STIC-D: algorithmic techniques for efficient parallel pagerank computation on real-world graphs][STIC-D algorithm]
- [PageRank Algorithm, Mining massive Datasets (CS246), Stanford University](http://snap.stanford.edu/class/cs246-videos-2019/lec9_190205-cs246-720.mp4)
- [SuiteSparse Matrix Collection]

<br>
<br>

[![](https://i.imgur.com/y1Q1Fzy.jpg)](https://www.youtube.com/watch?v=vbXTZlJ5fHU)

[SuiteSparse Matrix Collection]: https://suitesparse-collection-website.herokuapp.com
[STIC-D algorithm]: https://www.slideshare.net/SubhajitSahu/sticd-algorithmic-techniques-for-efficient-parallel-pagerank-computation-on-realworld-graphs
["graphs"]: https://github.com/puzzlef/graphs
[pull]: https://github.com/puzzlef/pagerank-push-vs-pull
[CSR]: https://github.com/puzzlef/pagerank-class-vs-csr
[charts]: https://photos.app.goo.gl/KzJK4wMtK9sJLRBWA
[sheets]: https://docs.google.com/spreadsheets/d/1AvibiNPO1pIC56ZMc16bRQ7E-afvvxGU2V_b7crgz0o/edit?usp=sharing
