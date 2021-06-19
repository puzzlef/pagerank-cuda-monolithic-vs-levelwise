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
# Loading graph /home/subhajit/data/soc-LiveJournal1.mtx ...
# order: 4847571 size: 68993773 {}
# order: 4847571 size: 69532892 {} (loopDeadEnds)
# order: 4847571 size: 69532892 {} (transposeWithDegree)
# [00289.403 ms; 000 iters.] [0.0000e+00 err.] pagerankNvgraph
# [00265.651 ms; 058 iters.] [2.7220e-06 err.] pagerankMonolithic
# [01627.724 ms; 050 iters.] [4.0653e-06 err.] pagerankLevelwise [1e+03 min-compute-size]
# [00533.757 ms; 050 iters.] [4.6830e-06 err.] pagerankLevelwise [5e+03 min-compute-size]
# [00387.058 ms; 051 iters.] [3.9963e-06 err.] pagerankLevelwise [1e+04 min-compute-size]
# [00263.821 ms; 051 iters.] [4.2981e-06 err.] pagerankLevelwise [5e+04 min-compute-size]
# [00246.427 ms; 051 iters.] [3.6271e-06 err.] pagerankLevelwise [1e+05 min-compute-size]
# [00252.093 ms; 056 iters.] [4.4768e-06 err.] pagerankLevelwise [5e+05 min-compute-size]
# [00249.986 ms; 056 iters.] [5.2331e-06 err.] pagerankLevelwise [1e+06 min-compute-size]
#
# ...
```

<br>

[![](https://i.imgur.com/kohs9Ov.png)][sheets]

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
