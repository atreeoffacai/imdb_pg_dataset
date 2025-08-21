# IMDB / JOB 工作负载

该仓库包含一个 Vagrant 虚拟机，它会自动下载并导入来自论文 [How Good are Query Optimizers, Really?](http://www.vldb.org/pvldb/vol9/p204-leis.pdf) 的 IMDB 数据集。请注意，在初始化时，虚拟机会下载超过 **1.2GB** 的数据。

它会创建一个运行 **Arch Linux** 的虚拟机，执行升级，安装最新版本的 **Postgres**，配置使用 **16GB 内存**（其中 \*\*12GB 分配给 Postgres 的 `shared_buffers`），分配 **4 个 CPU 核心**，并创建一个 **100GB 磁盘镜像** 来存储数据，最后下载并加载数据归档。⚠️ 该过程可能随时会失败。

注意：如果你只想下载一个 IMDB 数据集的 Postgres `pg_dump`，可以在这里获取：
[https://doi.org/10.7910/DVN/2QYZBT](https://doi.org/10.7910/DVN/2QYZBT)

要使用，请首先安装 [persistent storage Vagrant 插件](https://github.com/kusnier/vagrant-persistent-storage)：

```bash
vagrant plugin install vagrant-persistent-storage
```

接下来，修改 `vagrant/Vagrantfile`，设置数据库所在 VDI 文件的路径。

```ruby
config.persistent_storage.enabled = true
config.persistent_storage.location = "/PATH/TO/STORAGE/LOCATION.vdi"
config.persistent_storage.size = 100000
config.persistent_storage.mountname = 'pg'
config.persistent_storage.filesystem = 'ext4'
config.persistent_storage.mountpoint = '/media/data'
config.persistent_storage.volgroupname = 'myvolgroup'
```

然后启动虚拟机：

```bash
cd vagrant
vagrant up
cd ..
```

可以忽略最后几个关于 `/home/vagrant` 的警告。⚠️ 注意，该虚拟机会开启一个 Postgres 服务器，里面只有一个用户 `imdb`，没有密码。如果是在不安全的网络环境下运行，请务必加上防火墙或不要直接运行。

从宿主机连接到数据库：

```
psql -U imdb -h localhost
```

运行一个 JOB 查询：

```
psql -U imdb -h localhost < job/1a.sql
```

---

## 引用 (Citation)

如果你使用 **JOB 数据集**，请引用原始作者（无隶属关系）：

```bibtex
@article{JOB,
  series = {VLDB '15},
  title = {How {{Good Are Query Optimizers}}, {{Really}}?},
  volume = {9},
  issn = {2150-8097},
  doi = {10.14778/2850583.2850594},
  number = {3},
  journal = {Proc. VLDB Endow.},
  author = {Leis, Viktor and Gubichev, Andrey and Mirchev, Atanas and Boncz, Peter and Kemper, Alfons and Neumann, Thomas},
  month = nov,
  year = {2015},
  pages = {204--215}
}
```

如果你使用 **该虚拟机 (VM)** 或我们准备的数据集，请引用我们的论文：

```bibtex
@inproceedings{rejoin,
  address = {Houston, TX},
  series = {aiDM '18},
  title = {Deep {{Reinforcement Learning}} for {{Join Order Enumeration}}},
  shorttitle = {{{ReJOIN}}},
  booktitle = {First {{International Workshop}} on {{Exploiting Artificial Intelligence Techniques}} for {{Data Management}}},
  author = {Marcus, Ryan and Papaemmanouil, Olga},
  month = jun,
  year = {2018}
}
```

如果你使用 **CEB 数据集**，请引用 Flow Loss 论文：

> Parimarjan Negi, Ryan Marcus, Andreas Kipf, Hongzi Mao, Nesime Tatbul, Tim Kraska, and Mohammad Alizadeh. 2021. Flow-loss: learning cardinality estimates that matter. Proc. VLDB Endow. 14, 11 (July 2021), 2019–2032. [https://doi.org/10.14778/3476249.3476259](https://doi.org/10.14778/3476249.3476259)

```bibtex
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

如果你使用 **JOB 扩展查询 (Ext-JOB)**，请引用 Neo 论文：

> Ryan Marcus, Parimarjan Negi, Hongzi Mao, Chi Zhang, Mohammad Alizadeh, Tim Kraska, Olga Papaemmanouil, and Nesime Tatbul. 2019. Neo: a learned query optimizer. Proc. VLDB Endow. 12, 11 (July 2019), 1705–1718. [https://doi.org/10.14778/3342263.3342644](https://doi.org/10.14778/3342263.3342644)

```bibtex
@article{neo,
author = {Marcus, Ryan and Negi, Parimarjan and Mao, Hongzi and Zhang, Chi and Alizadeh, Mohammad and Kraska, Tim and Papaemmanouil, Olga and Tatbul, Nesime},
title = {Neo: A Learned Query Optimizer},
year = {2019},
issue_date = {July 2019},
publisher = {VLDB Endowment},
volume = {12},
number = {11},
issn = {2150-8097},
url = {https://doi.org/10.14778/3342263.3342644},
doi = {10.14778/3342263.3342644},
journal = {Proc. VLDB Endow.},
month = {jul},
pages = {1705–1718},
numpages = {14}
}
```

如果你使用 **JOB-D 查询**，请引用 HybridQO 论文（无隶属关系）：

```bibtex
@article{DBLP:journals/pvldb/YuC0L22,
  author       = {Xiang Yu and
                  Chengliang Chai and
                  Guoliang Li and
                  Jiabin Liu},
  title        = {Cost-based or Learning-based? {A} Hybrid Query Optimizer for Query
                  Plan Selection},
  journal      = {Proc. {VLDB} Endow.},
  volume       = {15},
  number       = {13},
  pages        = {3924--3936},
  year         = {2022},
  url          = {https://www.vldb.org/pvldb/vol15/p3924-li.pdf},
  doi          = {10.14778/3565838.3565846},
  timestamp    = {Mon, 23 Oct 2023 15:31:40 +0200},
  biburl       = {https://dblp.org/rec/journals/pvldb/YuC0L22.bib},
  bibsource    = {dblp computer science bibliography, https://dblp.org}
}
```
