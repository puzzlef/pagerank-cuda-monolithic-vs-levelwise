Design of **CUDA-based** *Levelwise PageRank algorithm* for link analysis.

[Levelwise PageRank] is the [STIC-D algorithm], without **ICD** optimizations.
We use a rank [pull] based approach, and perform the computation upon the [CSR]
representation of a graph on the GPU. We skip the computation of common teleport
contribution to all the vertices in the graph by simply adding self-loops to all
the vertices ([skip-teleport]). We process each component in a switched
thread/block-per-vertex fashion, with the vertices partitioned by in-degree. If
the size of a component is fewer than 5 million vertices, we process multiple
components together ([compute-5M]) using the switched approach.

For each experiment, we run all approaches on different types of graphs, running
each approach 5 times per graph to get a good time measure. The input data used
for the experiments is available at ["graphs"] (for small ones), and the
[SuiteSparse Matrix Collection]. Experiments were done with guidance from
[Prof. Dip Sankar Banerjee] and [Prof. Kishore Kothapalli].

<br>


### Adjusting Compute size

We then compare the performance between *Levelwise* CUDA-based PageRank with
various min. compute size, ranging from `1E+3` to `1E+7` ([adjust-compute-size]).
As mentioned above, min. compute is the minimum number of components processed
together in a switch thread/block-per-vertex fashion (using a two CUDA kernel
calls). From the results, it appears that a *min. compute size* of `5E+6` would
be a good choice, although there is no clear winner.

[adjust-compute-size]: https://github.com/puzzlef/pagerank-levelwise-cuda/tree/adjust-compute-size

<br>


### Comparision with Monolithic approach

In this experiment ([compare-monolithic], [main]), we compare the performance of
*Monolithic* vs *Levelwise* CUDA-based PageRank. On average, we observe that
*Levelwise* PageRank has around the *same* performance as the *Monolithic*
approach.

[compare-monolithic]: https://github.com/puzzlef/pagerank-levelwise-cuda/tree/compare-monolithic
[main]: https://github.com/puzzlef/pagerank-levelwise-cuda

<br>


### Other experiments

- [adjust-component-size](https://github.com/puzzlef/pagerank-levelwise-cuda/tree/adjust-component-size)

<br>


## References

- [STIC-D: algorithmic techniques for efficient parallel pagerank computation on real-world graphs][STIC-D algorithm]
- [PageRank Algorithm, Mining massive Datasets (CS246), Stanford University](https://www.youtube.com/watch?v=ke9g8hB0MEo)
- [SuiteSparse Matrix Collection]
- [Merge git repo into branch of another repo](https://stackoverflow.com/a/21353836/1413259)

<br>
<br>


[![](https://img.youtube.com/vi/riC9mRFp1ig/maxresdefault.jpg)](https://www.youtube.com/watch?v=riC9mRFp1ig)


[Prof. Dip Sankar Banerjee]: https://sites.google.com/site/dipsankarban/
[Prof. Kishore Kothapalli]: https://faculty.iiit.ac.in/~kkishore/
[Levelwise PageRank]: https://ieeexplore.ieee.org/abstract/document/9835216
[STIC-D algorithm]: https://dl.acm.org/doi/abs/10.1145/2833312.2833322
[SuiteSparse Matrix Collection]: https://suitesparse-collection-website.herokuapp.com
["graphs"]: https://github.com/puzzlef/graphs
[pull]: https://github.com/puzzlef/pagerank
[CSR]: https://github.com/puzzlef/pagerank
[skip-teleport]: https://github.com/puzzlef/pagerank-levelwise
[compute-5M]: https://github.com/puzzlef/pagerank-levelwise-cuda
[charts]: https://photos.app.goo.gl/xeZWBbSgBcCMDhDBA
[sheets]: https://docs.google.com/spreadsheets/d/1OMmcMTKi9TYyhyZBZjP9c7sceMAapPbyn-GW0gngn9k/edit?usp=sharing
