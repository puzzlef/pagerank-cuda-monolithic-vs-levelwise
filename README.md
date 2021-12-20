Comparing various min. compute sizes for topologically-ordered components
([componentwise CUDA]) PageRank ([pull], [CSR]).

`TODO!`

This experiment was for comparing performance between [componentwise CUDA] pagerank
with various **min. compute size**, ranging from `1E+3` - `1E+7`. Here,
**min. compute size** is the minimum no. nodes of each pagerank compute using
standard algorithm ([monolithic CUDA]). Each **min. compute size** was
attempted on different types of graphs, running each size 5 times per graph to
get a good time measure. **Componentwise** pagerank is the [STIC-D algorithm],
without **ICD** optimizations (using single-thread). Although there is no clear
winner, it appears a **min. compute size** of `5E+6` would be a good choice.

All outputs are saved in [out/](out/) and a small part of the output is listed
here. All [charts] are also included below, generated from [sheets]. The input
data used for this experiment is available at ["graphs"] (for small ones), and
the [SuiteSparse Matrix Collection].

<br>

```bash
$ nvcc -std=c++17 -Xcompiler -lnvgraph -O3 main.cu
$ ./a.out ~/data/min-1DeadEnd.mtx
$ ./a.out ~/data/min-2SCC.mtx
$ ...

# ...
#
# Loading graph /home/subhajit/data/soc-LiveJournal1.mtx ...
# order: 4847571 size: 68993773 {}
# order: 4847571 size: 69532892 {} (selfLoopDeadEnds)
# order: 4847571 size: 69532892 {} (transposeWithDegree)
# [00177.145 ms; 058 iters.] [0.0000e+00 err.] pagerankMonolithicCudaL1Norm
# [759097.500 ms; 047 iters.] [4.0881e-06 err.] pagerankComponentwiseCudaL1Norm [min-compute=1]
# [169912.156 ms; 048 iters.] [4.7450e-06 err.] pagerankComponentwiseCudaL1Norm [min-compute=5]
# [88768.242 ms; 048 iters.] [4.7864e-06 err.] pagerankComponentwiseCudaL1Norm [min-compute=10]
# [19623.629 ms; 049 iters.] [4.2578e-06 err.] pagerankComponentwiseCudaL1Norm [min-compute=50]
# [10715.938 ms; 049 iters.] [4.2451e-06 err.] pagerankComponentwiseCudaL1Norm [min-compute=100]
# [03362.187 ms; 050 iters.] [4.2470e-06 err.] pagerankComponentwiseCudaL1Norm [min-compute=500]
# [02024.559 ms; 050 iters.] [4.8736e-06 err.] pagerankComponentwiseCudaL1Norm [min-compute=1000]
# [01033.437 ms; 050 iters.] [4.7985e-06 err.] pagerankComponentwiseCudaL1Norm [min-compute=5000]
# [00938.964 ms; 051 iters.] [4.8210e-06 err.] pagerankComponentwiseCudaL1Norm [min-compute=10000]
# [00862.366 ms; 051 iters.] [4.4125e-06 err.] pagerankComponentwiseCudaL1Norm [min-compute=50000]
# [00850.893 ms; 051 iters.] [3.7797e-06 err.] pagerankComponentwiseCudaL1Norm [min-compute=100000]
# [00890.391 ms; 056 iters.] [4.2900e-06 err.] pagerankComponentwiseCudaL1Norm [min-compute=500000]
# [00889.220 ms; 056 iters.] [5.1174e-06 err.] pagerankComponentwiseCudaL1Norm [min-compute=1000000]
# [00906.149 ms; 058 iters.] [4.9725e-08 err.] pagerankComponentwiseCudaL1Norm [min-compute=5000000]
# [00909.675 ms; 058 iters.] [4.9725e-08 err.] pagerankComponentwiseCudaL1Norm [min-compute=10000000]
# [00905.678 ms; 058 iters.] [4.9725e-08 err.] pagerankComponentwiseCudaL1Norm [min-compute=50000000]
# [00094.423 ms; 031 iters.] [5.8269e-04 err.] pagerankMonolithicCudaL2Norm
# [741479.750 ms; 026 iters.] [7.7026e-04 err.] pagerankComponentwiseCudaL2Norm [min-compute=1]
# [157622.641 ms; 026 iters.] [7.6978e-04 err.] pagerankComponentwiseCudaL2Norm [min-compute=5]
# [82913.672 ms; 026 iters.] [6.4929e-04 err.] pagerankComponentwiseCudaL2Norm [min-compute=10]
# [17074.328 ms; 026 iters.] [7.6836e-04 err.] pagerankComponentwiseCudaL2Norm [min-compute=50]
# [09153.295 ms; 027 iters.] [6.4735e-04 err.] pagerankComponentwiseCudaL2Norm [min-compute=100]
# [02516.712 ms; 026 iters.] [7.6436e-04 err.] pagerankComponentwiseCudaL2Norm [min-compute=500]
# [01396.358 ms; 026 iters.] [6.4118e-04 err.] pagerankComponentwiseCudaL2Norm [min-compute=1000]
# [00581.809 ms; 026 iters.] [6.3411e-04 err.] pagerankComponentwiseCudaL2Norm [min-compute=5000]
# [00506.470 ms; 026 iters.] [6.3528e-04 err.] pagerankComponentwiseCudaL2Norm [min-compute=10000]
# [00422.770 ms; 025 iters.] [7.0286e-04 err.] pagerankComponentwiseCudaL2Norm [min-compute=50000]
# [00407.616 ms; 024 iters.] [7.2327e-04 err.] pagerankComponentwiseCudaL2Norm [min-compute=100000]
# [00382.745 ms; 024 iters.] [2.0932e-03 err.] pagerankComponentwiseCudaL2Norm [min-compute=500000]
# [00397.733 ms; 025 iters.] [1.7650e-03 err.] pagerankComponentwiseCudaL2Norm [min-compute=1000000]
# [00484.741 ms; 031 iters.] [5.8270e-04 err.] pagerankComponentwiseCudaL2Norm [min-compute=5000000]
# [00484.942 ms; 031 iters.] [5.8270e-04 err.] pagerankComponentwiseCudaL2Norm [min-compute=10000000]
# [00484.167 ms; 031 iters.] [5.8270e-04 err.] pagerankComponentwiseCudaL2Norm [min-compute=50000000]
# [00085.360 ms; 028 iters.] [1.0223e-03 err.] pagerankMonolithicCudaLiNorm
# [14588.019 ms; 012 iters.] [4.0536e-01 err.] pagerankComponentwiseCudaLiNorm [min-compute=1]
# [03565.822 ms; 012 iters.] [4.0314e-01 err.] pagerankComponentwiseCudaLiNorm [min-compute=5]
# [02099.776 ms; 012 iters.] [4.0151e-01 err.] pagerankComponentwiseCudaLiNorm [min-compute=10]
# [00711.914 ms; 012 iters.] [3.9896e-01 err.] pagerankComponentwiseCudaLiNorm [min-compute=50]
# [00505.077 ms; 012 iters.] [3.9304e-01 err.] pagerankComponentwiseCudaLiNorm [min-compute=100]
# [00310.393 ms; 013 iters.] [3.8109e-01 err.] pagerankComponentwiseCudaLiNorm [min-compute=500]
# [00272.909 ms; 013 iters.] [3.7051e-01 err.] pagerankComponentwiseCudaLiNorm [min-compute=1000]
# [00240.407 ms; 013 iters.] [3.0511e-01 err.] pagerankComponentwiseCudaLiNorm [min-compute=5000]
# [00234.785 ms; 013 iters.] [2.6698e-01 err.] pagerankComponentwiseCudaLiNorm [min-compute=10000]
# [00261.784 ms; 015 iters.] [1.3742e-01 err.] pagerankComponentwiseCudaLiNorm [min-compute=50000]
# [00263.119 ms; 016 iters.] [2.4241e-02 err.] pagerankComponentwiseCudaLiNorm [min-compute=100000]
# [00278.868 ms; 017 iters.] [1.9150e-02 err.] pagerankComponentwiseCudaLiNorm [min-compute=500000]
# [00307.975 ms; 019 iters.] [4.1948e-03 err.] pagerankComponentwiseCudaLiNorm [min-compute=1000000]
# [00437.383 ms; 028 iters.] [1.0223e-03 err.] pagerankComponentwiseCudaLiNorm [min-compute=5000000]
# [00437.980 ms; 028 iters.] [1.0223e-03 err.] pagerankComponentwiseCudaLiNorm [min-compute=10000000]
# [00437.369 ms; 028 iters.] [1.0223e-03 err.] pagerankComponentwiseCudaLiNorm [min-compute=50000000]
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

- [STIC-D: Algorithmic Techniques For Efficient Parallel Pagerank Computation on Real-World Graphs](https://gist.github.com/wolfram77/bb09968cc0e592583c4b180243697d5a)
- [Adjusting PageRank parameters and Comparing results](https://arxiv.org/abs/2108.02997)
- [PageRank Algorithm, Mining massive Datasets (CS246), Stanford University](https://www.youtube.com/watch?v=ke9g8hB0MEo)
- [SuiteSparse Matrix Collection]

<br>
<br>

[![](https://i.imgur.com/j3ml4cd.jpg)](https://www.youtube.com/watch?v=4Xw0MrllRfQ)

[Prof. Dip Sankar Banerjee]: https://sites.google.com/site/dipsankarban/
[Prof. Kishore Kothapalli]: https://www.iiit.ac.in/people/faculty/kkishore/
[SuiteSparse Matrix Collection]: https://sparse.tamu.edu
[monolithic CUDA]: https://github.com/puzzlef/pagerank-cuda-monolithic-vs-componentwise
[componentwise CUDA]: https://github.com/puzzlef/pagerank-cuda-monolithic-vs-componentwise
["graphs"]: https://github.com/puzzlef/graphs
[pull]: https://github.com/puzzlef/pagerank-push-vs-pull
[CSR]: https://github.com/puzzlef/pagerank-class-vs-csr
[charts]: https://photos.app.goo.gl/QLLLb1H2rRZiyv3i6
[sheets]: https://docs.google.com/spreadsheets/d/1yCK2S3_JDfSUk_rtAw59hQGWsbze7MR2SPKD6zzZiUA/edit?usp=sharing
