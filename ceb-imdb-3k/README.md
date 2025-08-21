# CEB IMDB “唯一计划” 3k 查询

这些 SQL 语句来自 [基数估计基准（cardinality estimation benchmark, CEB）](https://github.com/learnedsystems/CEB) 中的 IMDB 查询子集 —— “唯一计划（unique plans）” 的较小集合。根据 CEB 作者的说法，这个较小的集合已经 **“足够好（good enough）”** 用于初始实验。

如果你使用这些查询，请引用 Flow Loss 论文：

> Parimarjan Negi, Ryan Marcus, Andreas Kipf, Hongzi Mao, Nesime Tatbul, Tim Kraska, and Mohammad Alizadeh. 2021. Flow-loss: learning cardinality estimates that matter. Proc. VLDB Endow. 14, 11 (July 2021), 2019–2032. [https://doi.org/10.14778/3476249.3476259](https://doi.org/10.14778/3476249.3476259)

```
@article{flowloss,
author = {Negi, Parimarjan and Marcus, Ryan and Kipf, Andreas and Mao, Hongzi and Tatbul, Nesime and Kraska, Tim and Alizadeh, Mohammad},
title = {Flow-Loss: Learning Cardinality Estimates That Matter},
year = {2021},
issue_date = {July 2021},
publisher = {VLDB Endowment},
volume = {14},
number = {11},
issn = {2150-8097},
url = {https://doi.org/10.14778/3476249.3476259},
doi = {10.14778/3476249.3476259},
journal = {Proc. VLDB Endow.},
month = {jul},
pages = {2019–2032},
numpages = {14}
}
```

