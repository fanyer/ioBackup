---
title: echarts扩展之prepareBoxData详解
date: 2016-04-20 12:13:45
tags:
---



# echarts扩展之prepareBoxData详解


@(echarts)[箱线图|预处理|Markdown]

-------------------

   echarts官网只对非扩展模块做了文档和实例，其中箱线图BoxPLot和i官方内置模块，在componets目录下而大多数时候箱线图都会用到prepareBoxPlot这个模块，该模块位于extension/dataTool目录下，百度官方将echarts下载集成了prepareBoxPlot，但是没有文档和特殊说明，有时候会出一些问题/


	/*
	var low = boundIQR === 'none'
		? ascList[0]
		: Q1 - (boundIQR == null ? 1.5 : boundIQR) * IQR;
	var high = boundIQR === 'none'
		? ascList[ascList.length - 1]
		: Q3 + (boundIQR == null ? 1.5 : boundIQR) * IQR;
	*/


	


在使用百度提供的描点方法的时候，发现对箱线图的上下限确定有一些问题，并因此会导致outlier异常值的错误，这里我将箱线图的Min和Max描点改成了更为直观的Math上下限方法。

	//fanyer自定义
	var low = Math.max(ascList[0],Q1 - 1.5* IQR);
	
	var high = Math.min(ascList[ascList.length - 1],Q3 + 1.5 * IQR);
	
	//console.log(ascList[0]);
	//console.log(low);

	//fanyer自定义



