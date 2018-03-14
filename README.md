# RFM-Clustering 
* 利用RFM模型建模，并通过聚类分析、分类，分别算出8中不同的价值会员


## RFM模型构建会员价值标签

* R:最近一次消费(Recency)
* F:消费频率(Frequency)
* M:消费金额(Monetary)

## RFM的意义
* 在CRM中，经常会用到RFM模型分析去衡量以为会员的价值，和给企业带来的利润能力。这个模型是通过会员最近一次购买的时间段间隔、购买总金额，购买频率这三个因素来描述这会会员的价值状况。

## 基于RFM的零售行业会员聚类分析

### 因子：
* R：会员到门店消费的到目前为止的时间段，当R的值越大说明，会员上一次到门店的时间越大，则R越来大，与公司的价值是成负相关的。
* F：会员的消费频率，次数越多，利益越大，与公司的价值是成正相关的。
* M：会员消费的总金额，金额越大，利益越大，与公司的价值是成正相关的。

### 权重：
* MBA百科库中:研究邀请了被研究的某电信企业的两位地区经理、两位市场营销人员和一位长期客户应用文献的标度含义对RFM各指标权重进行比较分析。在分别得到五位评价者的两两比较矩阵后,采取取平均的方法得到下表的评价矩阵。


### 专家评分矩阵表
		R	F	M
	R	1	0.71	0.46
	F	1.41	1	0.85
	M	2.18	1.18	1

* 上表所示的两两比较矩阵的一致性比例C。 R < 0.1, 表明该判断矩阵的一致性可以接受。由上表得出RFM各指标相对权重为

![w](https://github.com/HarveyLau/RFM-Clustering/blob/master/img-storage/w%5E3.png)

* 其中M的权重最大,即专家们认为客户交费金额的高低是影响顾客价值高低的最主要因素。

### 分类
* 目标：使用K-means算法进行会员价值聚类，并加以RFM的指标，将具有相近终身价值的会员进行聚类。

### 步骤
1. 读取数据库中的数据（12个月），并清洗数据；
2. 将RFM中的三个指标，利用离差标准化将其数据标准化；

![FM](https://github.com/HarveyLau/RFM-Clustering/blob/master/img-storage/FM_score.png)

![R](https://github.com/HarveyLau/RFM-Clustering/blob/master/img-storage/R_score.png)

3. 应用AHP层次分析法来获取权重，并将各个指标加权；运用上述专家评定的评分矩阵：
4. 其中M的权重最大，即专家认为会员交易金额的高低是影响会员价值高低的最重要因素。
5. 根据CRM项目组的需求文案，确认聚类的类别的类别数量为K；
6. 将每类用户的RFM平均值和总的RFM平均值做比较，通过比较得到每类会员RFM的变动情况；
7. 分析会员的终身价值类别

	指标	最小值	最大值	平均值	标准差
	近度	2	128	60.07	20.191
	频度	0	13	5.98	1.861
	值度	54.43	1499.17	704.7467	216.22068
由于RFM三个指标的量纲不同，因此需要消除分布差异大的影响和量纲不同的影响。
### K-means数据聚类
K-means算法是很典型的基于距离的聚类算法，采用距离作为相似性的评价指标，即认为两个对象的距离越近，其相似度就越大。该算法认为簇是由距离靠近的对象组成的，因此把得到紧凑且独立的簇作为最终目标。
* 现在使用这三个因子作为本次建模的特征值（R、F、M），每个因子有两个变化，高与低，由此确认K的值：

![K的取值](https://github.com/HarveyLau/RFM-Clustering/blob/master/img-storage/k%3D2%5E3.png)

* 应用于每类价值的会员：

		R	F	M	Result
		0	0	0	流失客户
		0	0	1	一般维持客户
		0	1	0	新客户
		0	1	1	潜力客户
		1	0	0	重要挽留客户
		1	0	1	重要深耕客户
		1	1	0	重要唤醒客户
		1	1	1	重要价值客户

* 算法的实现K-means in Python
在Python或Spark Milb包中，已经有对K-means、K-means++成熟的集成，详细的聚类算法讲解，我将放在文献和附录里面。而这里我们使用的距离公式采用默认欧的几何公式来推算：

![DIS](https://github.com/HarveyLau/RFM-Clustering/blob/master/img-storage/dis.png)

## 会员终身价值得分（特征结合)
1.	AHP层次分析法		
2.	K-means(质心)		

* 总得分：

![C](https://github.com/HarveyLau/RFM-Clustering/blob/master/img-storage/C_score.png)

其中C是每一类的质心，按照总得分来进行标签逻辑






 
