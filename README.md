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
