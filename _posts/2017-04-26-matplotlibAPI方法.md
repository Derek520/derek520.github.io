---
layout: post
title: Matplotlib_API方法
categories: Matplotlib
description: Matplotlib_api
keywords: Matplotlib
comments: true
---

摘要： Matplotlib_Api方法,以及代码实现常用的绘图方法，其他绘制图形方法，可参考官网https://matplotlib.org/gallery/index.html

### 创建画布
    创建画布,并设置大小
    plt.figure(figsize=(20,8),dpi=100)
    创建子画布
    fig,axes = plt.subplots(nrows=1,ncols=2,figsize=(20,8),dpi=100)
    
    
### 保存图像
    plt.savefig("a.png")
    
### 设置轴刻度
    #设置x轴刻度
    plt.xticks(x[::2])
    #设置y轴刻度
    plt.yticks(range(min(y),max(y)+1,2))
### 替换x轴显示数据 plot
    plt.figure(figsize=(20,8),dpi=100)
    # 创建120个x数据
    x =range(120)
    # 每个x随机一个数字
    a = [random.randint(20,35) for i in x]
    plt.plot(x,a)
    
    _xticks = ["10点{}分".format(i) for i in x if i<60]
    _xticks += ["11点{}分".format(i-60) for i in x if i>60]
    # 替换x刻度,并且切片显示
    plt.xticks(x[::5],_xticks[::5])
    # 添加描述信息
    plt.xlabel("时间")
    plt.ylabel("温度")
    plt.title("温度时间变化图")
    plt.show()
### 双折线绘制方法，显示图例
    plt.figure(figsize=(20,8),dpi=100)
    x = range(11,31)
    a = [1,0,1,1,2,4,3,2,3,4,4,5,6,5,4,3,3,1,1,1]
    b = [1,0,3,1,2,2,3,3,2,1,2,1,1,1,1,1,1,1,1,1]
    
    # 双折线，color改变颜色、linewidth大小，alpha透明度，linestyle显示样式，和label图例名
    plt.plot(x,a,color='r',linewidth=4,alpha=0.5,linestyle=':',label = '我')
    plt.plot(x,b,color='g',linestyle="-.",label='朋友')
    
    _xticks = ["{}岁".format(i) for i in x]
    plt.xticks(x,_xticks)
    plt.xlabel("年龄")
    plt.ylabel("朋友个数")
    plt.title("走势图")
    # 显示图例
    plt.legend(loc=0)
    plt.show()
### 两个双折线图，分开显示，并添加水印
    
    def set_ax(ax):
        plt.sca(ax)
        _xticks = ["{}岁".format(i) for i in x]
        plt.xticks(x,_xticks)
        plt.xlabel("年龄")
        plt.ylabel("朋友")
        # 图例显示
        plt.legend(loc=0)
    
        plt.annotate(
            '最高点:为6',  # 显示字符串
            xy=(23, 6),  # 箭头位置
            xytext=(26,6 ),  # 文本位置
            arrowprops=dict(facecolor='red', shrink=0.1, width=2)  # facecolor:箭头颜色；shrink:箭头的起始和结束位置两侧的空白大小；width:箭头宽度
        )

    #创建子图像(可以在一个画板上创建多个图像)
    #subplots开启子画布后，plt会默认将最后一个axes作为基准
    # nrows一行，ncols两列
    fig,axes = plt.subplots(nrows=1,ncols=2,figsize=(20,8),dpi=100)
    print(axes)
    print(fig)
    x = range(11,31)
    # 两个数据
    a = [1,0,1,1,2,4,3,2,3,4,4,5,6,5,4,3,3,1,1,1]
    b = [1,0,3,1,2,2,3,3,2,1,2,1,1,1,1,1,1,1,1,1]
    # axes两个元素，代表连个画布
    axes[0].plot(x,a,color="r",linewidth=4,linestyle=":",alpha=0.5,label="我")
    axes[1].plot(x,b,color="g",linestyle="-.",label="同桌")
    
    set_ax(axes[0])
    set_ax(axes[1])
    
    # 添加水印
    fig.text(0.4,0.5,"个人专属",fontsize=40,color="gray",alpha=0.5)
    plt.show()

### 创建散点图 scatter
    plt.figure(figsize=(20,8),dpi=100)
    x = range(31)
    a = [11,17,16,11,12,11,12,6,6,7,8,9,12,15,14,17,18,21,16,17,20,14,15,15,15,19,21,22,22,22,23]
    b = [26,26,28,19,21,17,16,19,18,20,20,19,22,23,17,20,21,20,22,15,11,15,5,13,17,10,11,13,12,13,6]
    
    x1 = range(1,32)
    x2 = range(51,82)
    # 绘制散点图
    plt.scatter(x1,a)
    plt.scatter(x2,b)
    _x = list(x1)+list(x2)
    _xticks = ["3月{}日".format(i) for i in x1]
    _xticks += ["10月{}日".format(i) for i in x1]
    plt.xticks(_x[::3],_xticks[::3],rotation=45)
    plt.show()
### 绘制条形图 bar\barh
    plt.figure(figsize=(20,8),dpi=100)
    a = ["战狼2","速度与激情8","功夫瑜伽","西游伏妖篇","变形金刚5：最后的骑士","摔跤吧！爸爸","加勒比海盗5：死无对证","金刚：骷髅岛","极限特工：终极回归","生化危机6：终章","乘风破浪","神偷奶爸3","智取威虎山","大闹天竺","金刚狼3：殊死一战","蜘蛛侠：英雄归来","悟空传","银河护卫队2","情圣","新木乃伊",]
    b=[56.01,26.94,17.53,16.49,15.45,12.96,11.8,11.61,11.28,11.12,10.49,10.3,8.75,7.55,7.32,6.99,6.88,6.86,6.58,6.23]
    _x = range(len(a))
    
    # 竖着显示
    plt.bar(_x,b)
    plt.xticks(_x,a,rotation=45)
    plt.xlabel("电影")
    plt.ylabel("票房")
    plt.title("电影票房统计")
    # 横着显示
    # plt.barh(_x,b)
    # plt.yticks(_x,a)
    # plt.ylabel("电影")
    # plt.xlabel("票房")
    # plt.title("电影票房统计")
    plt.show()
### 绘制多条条形图 对比
    plt.figure(figsize=(20,8),dpi=100)
    a = ["猩球崛起3：终极之战","敦刻尔克","蜘蛛侠：英雄归来","战狼2"]
    b_16 = [15746,312,4497,319]
    b_15 = [12357,156,2045,168]
    b_14 = [2358,399,2358,362]
    
    bar_width = 0.2
    
    
    #后面绘制的条形图比前面挨着的那个条形图多bar_width
    x_14 = range(len(a))
    x_15 = [i+bar_width for i in x_14]
    x_16 = [i+bar_width for i in x_15]
    
    plt.bar(x_14,b_14,width=bar_width)
    plt.bar(x_15,b_15,width=bar_width)
    plt.bar(x_16,b_16,width=bar_width)
    
    plt.xticks(x_15,a)
    plt.show()
    
### 绘制直方图grid
    plt.figure(figsize=(20,8),dpi=100)
    a=[131,  98, 125, 131, 124, 139, 131, 117, 128, 108, 135, 138, 131, 102, 107, 114, 119, 128, 121, 142, 127, 130, 124, 101, 110, 116, 117, 110, 128, 128, 115,  99, 136, 126, 134,  95, 138, 117, 111,78, 132, 124, 113, 150, 110, 117,  86,  95, 144, 105, 126, 130,126, 130, 126, 116, 123, 106, 112, 138, 123,  86, 101,  99, 136,123, 117, 119, 105, 137, 123, 128, 125, 104, 109, 134, 125, 127,105, 120, 107, 129, 116, 108, 132, 103, 136, 118, 102, 120, 114,105, 115, 132, 145, 119, 121, 112, 139, 125, 138, 109, 132, 134,156, 106, 117, 127, 144, 139, 139, 119, 140,  83, 110, 102,123,107, 143, 115, 136, 118, 139, 123, 112, 118, 125, 109, 119, 133,112, 114, 122, 109, 106, 123, 116, 131, 127, 115, 118, 112, 135,115, 146, 137, 116, 103, 144,  83, 123, 111, 110, 111, 100, 154,136, 100, 118, 119, 133, 134, 106, 129, 126, 110, 111, 109, 141,120, 117, 106, 149, 122, 122, 110, 118, 127, 121, 114, 125, 126,114, 140, 103, 130, 141, 117, 106, 114, 121, 114, 133, 137,  92,121, 112, 146,  97, 137, 105,  98, 117, 112,  81,  97, 139, 113,134, 106, 144, 110, 137, 137, 111, 104, 117, 100, 111, 101, 110,105, 129, 137, 112, 120, 113, 133, 112,  83,  94, 146, 133, 101,131, 116, 111,  84, 137, 115, 122, 106, 144, 109, 123, 116, 111,111, 133, 150]
    
    #分组：组数
    #设置成多少组合适？
    #组数=极差/组距
    #极差：最大值-最小值
    
    #组距：5
    d = 5
    # 必须是一个整数
    num_bins = (max(a)-min(a))//d
    
    # 参数1：原始数据
    # 参数2：组数
    plt.hist(a,num_bins)
    
    plt.xticks(range(min(a),max(a)+d)[::3])
    # 绘制直方图grid
    plt.grid(alpha=0.4,linestyle="-.")
    plt.show()

### 绘制饼状图pie
    plt.figure(figsize=(20,8),dpi=100)
    movie_name = ['雷神3：诸神黄昏','正义联盟','东方快车谋杀案','寻梦环游记','全球风暴',
    '降魔传','追捕','七十七天','密战','狂兽','其它']
    place_count = [60605,54546,45819,28243,13270,
    9945,7679,6799,6101,4621,20105]
    # 参数1：数据
    # 参数2：名字
    # 参数3： 百分比
    # 参数4：饼图颜色
    plt.pie(place_count,labels=movie_name,autopct="%3.2f%%",colors=['b','r','g','y','c','m','y','k','c','g','g'])
    
    # 保证饼状图是圆的
    plt.axis('equal')
    # 添加图例，loc：表示信息的位置
    plt.legend(loc="upper left")
    plt.show()
