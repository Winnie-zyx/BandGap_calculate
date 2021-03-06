# 介绍
这是一个根据输入的不同U值获得材料带隙值的shell脚本，其工作主要步骤如下：
## 主要步骤：
1. 进行结构优化(optimize)获得更为合理的晶体结构(CONTCAR)
2. 利用优化后结果进行静态计算(static)，获得波函数(WAVECAR)和电子态密度函数(CHGCAR)信息，为后续能带计算做准备
3. 能带计算(band)获得材料带隙值

![不同U值对应带隙与理论带隙值比较](http://photo.cyicz123.com/%E4%B8%8D%E5%90%8CU%E5%80%BC%E5%AF%B9%E5%BA%94%E5%B8%A6%E9%9A%99%E4%B8%8E%E7%90%86%E8%AE%BA%E5%B8%A6%E9%9A%99%E5%80%BC%E6%AF%94%E8%BE%83.png)

## 计算原理
我们运用基于密度泛函理论（DFT）的第一性原理计算方法来求解材料的电子结构。采用计算软件维也纳从头算模拟程序包（VASP），通过投影缀加平面波PAW方法描述电子与离子间相互作用，并使用广义梯度近似方法（GGA)作为合理近似方法处理电子间相互排斥作用。该方法已在材料的晶体结构、电子结构以及材料的力学性能等方面取得了巨大成功，然而在计算Mott绝缘体（如过渡金属氧化物和稀土氧化物）时，由于其d、f轨道电子的强关联作用，往往各类性质的决定性参数是Hubbard参数U，但传统的第一性原理计算只考虑了交换参数J，未考虑U，导致计算的失败。

![图一 一种Mott绝缘体——TiO2](http://photo.cyicz123.com/%E4%B8%80%E7%A7%8DMott%E7%BB%9D%E7%BC%98%E4%BD%93%E2%80%94%E2%80%94TiO2.jpg "图一 一种Mott绝缘体——TiO2")

Anisimov等人提出的加U方法将所研究的电子分为不考虑Hubbard参数U以及对于d、f轨道电子考虑强关联作用的两部分。目前GGA+U方法作为GGA方法的补充，很好地处理了电子之间的强关联效应，已在强关联体系的计算方面取得了很大的成功。

![图二 LDA+U校正示意图](http://photo.cyicz123.com/LDA%2BU%E6%A0%A1%E6%AD%A3%E7%A4%BA%E6%84%8F%E5%9B%BE.jpg)

如何考察GGA+U的U值应该设为多少？目前主流的指标有三种，晶格常数，带隙值，磁矩。通过将计算模拟所得的相关参数值与实验值相比较，选择使相关指标最接近实验值的U值作为理想U值。大多数情况下，带隙值具有极大参考意义，对于大多数需要使用GGA+U方法的半导体，带隙值对U值变化非常敏感，而磁矩指标只有在材料具有磁矩的情况下才适用，对于无磁性材料完全无效。于是我们给出以带隙值为判据的U值测试方法，更加快捷筛选出理想U值。

![图三 从能带图中获得带隙值](http://photo.cyicz123.com/%E4%BB%8E%E8%83%BD%E5%B8%A6%E5%9B%BE%E4%B8%AD%E8%8E%B7%E5%BE%97%E5%B8%A6%E9%9A%99%E5%80%BC.png)

# 快速开始
脚本依赖于计算软件vasp、 vaspkit。
1. git clone https://github.com/cyicz123/BandGap_calculate.git
2. chmod +x calculate.sh
3. ./calculate.sh -h或者./calculate.sh --help获取帮助

![帮助界面](http://photo.cyicz123.com/%E8%84%9A%E6%9C%AC%E5%B8%AE%E5%8A%A9.png)

4. ./calculate.sh U值1 U值2...
5. 等待结果
6. 最后Band Gap的输出会汇总在report.txt文件里
# 贡献
* 脚本由cyicz123编写，计算材料学原理由张奕羲提供
* 使用遇到问题可以通过issues反馈
