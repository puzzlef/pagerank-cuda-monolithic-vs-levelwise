Comparing various min. component sizes for topologically-ordered components
(levelwise) PageRank ([pull], [CSR]).

This experiment was for comparing performance between:
1. Find **levelwise** pagerank using **min. component size** from `1` - `1E+7`.

Each **min. component size** was attempted on different types of graphs,
running each size 5 times per graph to get a good time measure. **Levelwise**
pagerank is the [STIC-D algorithm], without **ICD** optimizations (using
single-thread). Although there is no clear winner, it appears a
**min. component size** of `50` would be a good choice.

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

[![](https://i.imgur.com/awWEd8m.png)][sheets]

<br>
<br>


## References

- [STIC-D: algorithmic techniques for efficient parallel pagerank computation on real-world graphs][STIC-D algorithm]
- [PageRank Algorithm, Mining massive Datasets (CS246), Stanford University](http://snap.stanford.edu/class/cs246-videos-2019/lec9_190205-cs246-720.mp4)
- [SuiteSparse Matrix Collection]

<br>
<br>

[![](https://i.imgur.com/1VFZdqh.jpg)](https://www.youtube.com/watch?v=vbXTZlJ5fHU)

[pull]: https://github.com/puzzlef/pagerank-push-vs-pull
[CSR]: https://github.com/puzzlef/pagerank-class-vs-csr
[STIC-D algorithm]: https://www.slideshare.net/SubhajitSahu/sticd-algorithmic-techniques-for-efficient-parallel-pagerank-computation-on-realworld-graphs
[charts]: https://photos.app.goo.gl/KveUUSpamrPKPmvY6
[sheets]: https://docs.google.com/spreadsheets/d/1cdH3LURJo4KfflTF0grHtICUsaEmDHxKGy4Vti4eZc8/edit?usp=sharing
["graphs"]: https://github.com/puzzlef/graphs
[SuiteSparse Matrix Collection]: https://suitesparse-collection-website.herokuapp.com
