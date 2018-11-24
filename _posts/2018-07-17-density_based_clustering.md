---
title: "密度聚类"
author: Zhang Keke
date: 2018-07-17
categories:
  - MACHINE LEARNLING
tags:
  - math
  - mechine learning
---

`密度聚类假设：聚类结构能通过样本分布的紧密程度来确认`

密度聚类核心概念：
设给定数据集$D=\{x_1, x_2,x_3 \cdots x_m \}$

$\epsilon$领域：对于$x_j \in D $， $x_j$ 的$\epsilon$领域内的数据点集合为：

$$N_{\epsilon}(x_j) = \{x_i \in D | dist(x_j,x_i) \leq \epsilon \}$$


核心对象：若$\|N_{\epsilon}(x_j) \| \geq P_{min}$，则 $x_j$为核心对象

密度直达：若$x_i$在$x_j$的领域内，且，$x_j$为核心对象，则称$x_i$为$x_j$的密度直达。

密度可达：若$x_i$可以通过$x_j$一条，一条的密度直达连接，则称$x_j$为$x_j$的密度可达。

密度相连：若存在某点$x_k$使$x_i, x_j$均为$x_k$的密度可达，则称$x_i, x_j$为密度相连。

密度簇：通过密度可达导出的集合，集合内任意一点都能在此集合内找到另外一点是此点的密度直达或能密度直达到此点的点。集合外不存在与簇内密度相连的点。不属于任何簇的点为噪声或异常值


#### 定义距离：
金额和时间在距离的影响是不等价的，时间优先。同时鉴于只有两维数据，采用乘法连接两方权重，此方法能把特征空间非线性的映射到更大的距离空间，而且数据只有两维，不会因为连乘导致上溢。维度多的数据不适用此距离公式。

$x_i =(amount,time)_i = (a_i,t_i)$
$$dist(x_i,x_j)= (|a_i-a_j|+1) \times (|t_i-t_j|)$$

加入权重（1，0）消除金额差为0时的导致时间效用为0的缺点，始终保证时间的效应存在并影响距离

或可采用：
$$dist(x_i,x_j)= (|a_i-a_j|+1)*0.3 + (|t_i-t_j|) *0.7$$

#### 密度聚类样板代码

``` python
import numpy as np
from sklearn.datasets import load_iris
from functools import reduce
def dist(x):
	"""
	Distance = |a-b|+weight
	:param x: np.array[n_points * features]
	:return: np.array[n_points * n_points]
	"""
	leng = x.shape[0]
	weight = np.array([0, 0, 0, 1])
	dis_map = np.zeros((leng, leng))
	for i in range(leng):
		for j in range(leng):
			dis_map[i, j] = np.prod(np.abs(x[i] - x[j]) + weight)
	return dis_map
	
if __name__ == "__main__":
	data = load_iris()
	X = data.data[:100]
	Y = data.target[:100]
	theta = 0.1
	minp = 30
	dis_map = dist(X)
	cores = dis_map.copy()
	cores[cores > theta] = 0
	core_list = []
	n_reachables = np.sum(np.sign(cores), 1)
	for i, j in enumerate(n_reachables):
		if j > minp:
			core_list.append(i)
	cores_set = set(core_list)
	visited = set()
	clusters = []
	while cores_set:
		ss = cores_set.pop()
		que = set([ss])
		pre_visited = visited.copy()
		while que:
			j = que.pop()
			visited.update([j])
			if j in core_list:
				c = np.argwhere(cores[j] > 0)
				ad_join = reduce(lambda x, y: x + y, c.tolist())
				que.update(set(ad_join) - visited)
		clusters.append(visited - pre_visited)
		cores_set = cores_set - visited
```