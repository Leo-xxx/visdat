## Github项目推荐 | visdat - 数据初步探索性可视化工具

AI研习社 [AI研习社](javascript:void(0);) *4天前*

![img](https://mmbiz.qpic.cn/mmbiz_jpg/bicdMLzImlibRiboYcgtAAFwZvvLPUlRkFmiaQ8aCfWBsYib2ic7uVBLAHBtL8m8gYWxDLRdVWaAoASYXjjYclph6NlQ/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**visdat - Preliminary Exploratory Visualisation of Data**

by **rOpenSci**

**Site：**http://visdat.njtierney.com/

![1558944333832349.png](https://mmbiz.qpic.cn/mmbiz_png/bicdMLzImlibSfRR6IYfX2tAY2xUnbszRUE1FrRNcmw9rZUe0DLx8ZXkoLLKLOwZmkYRUdXTozHJzcm5nnJQULIw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

## **如何安装？**

你可以在CRAN获取visdat

- 

```
install.packages("visdat")
```

如果您想使用开发版本，请从github安装：

- 
- 

```
# install.packages("devtools")devtools::install_github("ropensci/visdat")
```



## **visdat能做什么？**

vis_dat最初受到csv-fingerprint的启发，通过使用vis_dat将数据框中的变量类显示为带有vis_dat的绘图，并使用vis_miss简要查看丢失的数据模式，vis_dat将帮助你可视化数据框并“查看数据”。

**visdat 的六大特点如下：**

- vis_dat()将数据框可视化，显示列的类别，并显示缺少的数据。
- vis_miss()只显示缺失的数据，并允许对缺失进行聚类并重新排列列。 vis_miss()类似于mi包中的missing.pattern.plot。 然而不幸的是，missing.pattern.plot已经不再出现在mi包中（截至2016年2月14日）。
- vis_compare()将相同维度的两个数据帧之间的差异可视化
- vis_expect()将数据中某些条件成立的位置可视化
- vis_cor()在一个漂亮的热图中对变量的相关性可视化
- vis_guess()将数据中各个类的earch值可视化

你可以在“using visdat”小节中查看更多关于visdat的信息。

请注意，本项目随着贡献者行为准则一起发布。 参与此项目即表示同意遵守其条款。



## **示例**

- ### **使用** **vis_dat()**

让我们看看基地R的airquality（空气质量）数据集中的内容，其中包含有关1973年5月至9月纽约每日空气质量测量的信息。有关数据集的更多信息可以在 ?airquality中找到。

- 
- 
- 

```
library(visdat)
vis_dat(airquality)
```

![1558944880525484.png](https://mmbiz.qpic.cn/mmbiz_png/bicdMLzImlibSfRR6IYfX2tAY2xUnbszRUkmXC8iaV5jpnU9qvdNlD1ia8ibXnn0rl0ZibHsEgWJ0Hy1hic1IT5XI2QBA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

上面的图告诉我们，R读取这个数据集时是数值和整数值，并在Ozone和Solar.R中显示一些缺失的数据。类在图例中表示，缺失的数据用灰色表示，列/变量名列在x轴上。



- ### **使用** **vis_miss()**

我们可以使用vis_miss()进一步探索缺失的数据：

- 

```
vis_miss(airquality)
```

![1558944938773472.png](https://mmbiz.qpic.cn/mmbiz_png/bicdMLzImlibSfRR6IYfX2tAY2xUnbszRU7EXQApzYGMM1fBtTWmNoJaQSw5micY5f9IF3XljSACP6v8Diaj670bgA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

vis_miss中缺失/完成的百分比精确到小数点后1位。

你可以通过设置cluster = TRUE来对缺失进行聚类：

- 
- 

```
vis_miss(airquality,          cluster = TRUE)
```

![1558945083428202.png](https://mmbiz.qpic.cn/mmbiz_png/bicdMLzImlibSfRR6IYfX2tAY2xUnbszRUbbib03u4yxM9ZicBToAKsSvkluCOmib6IHn5nENbViaevXAFHanxAYqRGQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

通过设置sort_miss = TRUE，数据列也可以按缺失最多的列进行排列：

- 
- 

```
vis_miss(airquality,         sort_miss = TRUE)
```

![1558945121343445.png](https://mmbiz.qpic.cn/mmbiz_png/bicdMLzImlibSfRR6IYfX2tAY2xUnbszRU7EXQApzYGMM1fBtTWmNoJaQSw5micY5f9IF3XljSACP6v8Diaj670bgA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

vis_miss表示当缺失率<0.1％时，缺少数据的数量非常少：

- 
- 
- 
- 
- 

```
test_miss_df <- data.frame(x1 = 1:10000,                           x2 = rep("A", 10000),                           x3 = c(rep(1L, 9999), NA))
vis_miss(test_miss_df)
```

![1558945224181416.png](https://mmbiz.qpic.cn/mmbiz_png/bicdMLzImlibSfRR6IYfX2tAY2xUnbszRUdyh0tD1xiakXnK3jJzVhLdReCMicc3xS6ceGFSrV5FIibAM4t66HFW7ew/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

vis_miss还将提示何时没有丢失数据：

- 

```
vis_miss(mtcars)
```

![1558945263289157.png](https://mmbiz.qpic.cn/mmbiz_png/bicdMLzImlibSfRR6IYfX2tAY2xUnbszRURE5z4QC1uLSu0NT2f9ytrC76vJ8R9uAWicib9vjrQPOTzpmFiaQhRVnRg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

为了进一步探索数据集中的缺失结构，我推荐使用naniar包，它为缺失值的图形和数值探索提供了更多通用工具。



- ### **使用****vis_compare()**

有时你想要查看数据中发生了哪些变化。 vis_compare()可以显示两个相同大小的数据帧的差异。 我们来看一个例子：

让我们对chickwts做一些修改，并比较这个新的数据集：

- 
- 
- 
- 
- 

```
set.seed(2019-04-03-1105)chickwts_diff <- chickwtschickwts_diff[sample(1:nrow(chickwts), 30),sample(1:ncol(chickwts), 2)] <- NA
vis_compare(chickwts_diff, chickwts)
```

![1558945390680455.png](https://mmbiz.qpic.cn/mmbiz_png/bicdMLzImlibSfRR6IYfX2tAY2xUnbszRU2Q5W2HMJLgTKGqfzNldZR5uJ6hhqKIqJZBaggpsyn1C1UGnubAlSHA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

这里的差异会用蓝色标出。

如果你尝试在尺寸不同时比较差异，则会出现一个非常难看的错误：

```

```

- 
- 
- 
- 
- 
- 

```
chickwts_diff_2 <- chickwtschickwts_diff_2$new_col <- chickwts_diff_2$weight*2
vis_compare(chickwts, chickwts_diff_2)# Error in vis_compare(chickwts, chickwts_diff_2) : #   Dimensions of df1 and df2 are not the same. vis_compare requires dataframes of identical dimensions.
```

篇幅有限，如需查看更多使用示例，请访问Github项目查看。



**Github项目地址：**

**https://github.com/ropensci/visdat**



![1558945462677431.png](https://mmbiz.qpic.cn/mmbiz_png/bicdMLzImlibSfRR6IYfX2tAY2xUnbszRUP2uSM25VzibsOJ0fN3iblFjmeAGNt1qSNVqicGYJRliaZqtgIxS6cm7Org/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**- 往 期 内 容 推 荐 -**

**● 学界 | ACM对2018图灵奖获得者Geoffrey Hinton、Yann LeCun、Yoshua Bengio的专访**

**● 搜狗搜索 “AIS 2019” 论文研讨会回放观看 & 嘉宾 PPT 打包下载**

**● 20分钟了解TensorFlow基础**

**● CVPR 2019 Oral 论文解读 | 利用事件相机将模糊视频还原成高速清晰视频**



![img](https://mmbiz.qpic.cn/mmbiz_gif/bicdMLzImlibRAS3Tao2nfeJk00qqxX3axIgPV3yia4NPESGdUJEM9vsfw1O4Dg1iat7lVNAmbCMY65ia2pzfBXm5kg/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1) 点击 **阅读原文** ，查看 CVPR 2019 Oral 论文解读 | 百度提出关于网络压缩和加速的新剪枝算法

[阅读原文](https://mp.weixin.qq.com/s?__biz=MjM5ODU3OTIyOA==&mid=2650676808&idx=3&sn=ed9624c13948b8dc37afc47859119761&chksm=bec2233b89b5aa2d1db2cf457fac7491842f2ee1d31d2f721841cd1c7dadc4183a4be6634510&mpshare=1&scene=1&srcid=0530oTboicmymU1GlHsvxtaK&key=c47853a08ff0b5df26b154eda5f22946d27654e39a8477f7ad9dddd6ebcff3acd903c905932e7d514f6a4597edb925fa5d26c88b046b6252ca28482371ece803e127cf1ef193d5674174524889027084&ascene=1&uin=MjMzNDA2ODYyNQ%3D%3D&devicetype=Windows+10&version=62060833&lang=zh_CN&pass_ticket=%2BtDZ2Al0VM5wjz5XAzAxV1jJFwepKB91N4744YqAfvwEIleHxJyeJlLibQdxfrJN##)







微信扫一扫
关注该公众号