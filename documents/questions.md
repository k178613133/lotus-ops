# 问题整理

下面有一些问题是
1.daemon的部署 - max
我们原来是2台daemon机器互备,单miner挂一个节点
现在是否只需要一个有转发到公网的daemon,剩下的一个机器可以用做seal miner上

2.分布式miner的部署,我看到是需要起 winning,wdpost,seal 3个miner.其中一个miner开 sectorId获取即可 - max
我们原来是2台miner机器互备,一台miner多插了点SSD临时当worker
现在是否 一台作为 winning miner
另外一台作为 wdpost miner
然后把 seal miner 放到上述的一个 daemon机器上即可
其中sectorId获取也可以放到 seal miner 上
如果需要 deal miner 如何部署,能否给一些建议

3.worker的部署.我们需要 AP-PC1绑定.但是 PC1-PC2就无法绑定了.全部需要内网传输到 gpu机器 - xy
这里每个 worker 机器原来是并行 30个 lotus-worker进程,每个worker单独只做一个sector的p1,开了 SDR , SDR_PRODUCERS设置为1
但是我看了文档中说的 FIL_PROOFS_USE_MULTICORE_SDR、FIL_PROOFS_MULTICORE_SDR_PRODUCERS、ENV_CPU_CORE_BEGIN_NUM、ENV_CPU_CORE_END_NUM环境变量
其中 后两个是软件新增的是把.而且也建议 7302 把 FIL_PROOFS_MULTICORE_SDR_PRODUCERS 设为 2 ,是这样嘛
那我现在应该怎么部署,希望是用满2T内存的并发,开SDR
a.是起一个 lotus-worker 还是依然30个 lotus-worker 并行
b.SDR 和上述的4个环境变量如何设置
c.我们原来worker也放了 proof和proof cache 证明参数的文件,看文档是否只有 daemon miner c2 需要.这个没有尝试过.

4.gpu机器的部署.原来是8卡机起了8个 lotus-worker 通过 CUDA_visible 配置绑定gpu - mje
现在是否可以,并且是否需要单卡并行 环境变量NUM_HANDLES、NUM_KERNELS 如何设置

5.worker和gpu不通过 seal miner 直接落盘到 nfs存储如何实现 - mje

6.scheduler的配置中 AutoPledgeDiff 是什么意义 - xy
自动化添加封装 lotus-miner sectors mypledge 的使用方式,该命令的后果是如何

7.显卡驱动和cuda是否需要变更 - mje

8.如果在部署新程序中遇到问题，已经部署了一半发现无法继续，是否可以快速还原到官方版本 - max + xy