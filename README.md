Comparing various min. compute sizes for topologically-ordered components
([levelwise CUDA]) PageRank ([pull], [CSR]).

This experiment was for comparing performance between [levelwise CUDA] pagerank
with various **min. compute size**, ranging from `1E+3` - `1E+7`. Here,
**min. compute size** is the minimum no. nodes of each pagerank compute using
standard algorithm ([monolithic CUDA]). Each **min. compute size** was
attempted on different types of graphs, running each size 5 times per graph to
get a good time measure. **Levelwise** pagerank is the [STIC-D algorithm],
without **ICD** optimizations (using single-thread). Although there is no clear
winner, it appears a **min. compute size** of `5E+6` would be a good choice.

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

[![](https://i.imgur.com/Mufuphe.png)][sheets]
[![](https://i.imgur.com/eAVrM2S.png)][sheets]
[![](https://i.imgur.com/vGwZuBS.png)][sheets]
[![](https://i.imgur.com/PyXG9Fk.png)][sheets]

<br>
<br>


## References

- [STIC-D: algorithmic techniques for efficient parallel pagerank computation on real-world graphs][STIC-D algorithm]
- [PageRank Algorithm, Mining massive Datasets (CS246), Stanford University](http://snap.stanford.edu/class/cs246-videos-2019/lec9_190205-cs246-720.mp4)
- [SuiteSparse Matrix Collection]

<br>
<br>

[![](https://i.imgur.com/j3ml4cd.jpg)](https://www.youtube.com/watch?v=4Xw0MrllRfQ)

[SuiteSparse Matrix Collection]: https://suitesparse-collection-website.herokuapp.com
[STIC-D algorithm]: https://www.slideshare.net/SubhajitSahu/sticd-algorithmic-techniques-for-efficient-parallel-pagerank-computation-on-realworld-graphs
[monolithic CUDA]: https://github.com/puzzlef/pagerank-cuda-monolithic-vs-levelwise
[levelwise CUDA]: https://github.com/puzzlef/pagerank-cuda-monolithic-vs-levelwise
["graphs"]: https://github.com/puzzlef/graphs
[pull]: https://github.com/puzzlef/pagerank-push-vs-pull
[CSR]: https://github.com/puzzlef/pagerank-class-vs-csr
[charts]: https://photos.app.goo.gl/QLLLb1H2rRZiyv3i6
[sheets]: https://docs.google.com/spreadsheets/d/1LzuNes4EUm1t5Zl8Oq2_lZAAnOSWlpj19ShV-xtc3Cs/edit?usp=sharing
