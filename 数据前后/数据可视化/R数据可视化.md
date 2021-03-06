
----------

# R数据可视化
## R数据预处理
### 数据结构
+	数值，字符，逻辑
+	整数，浮点，日期，因子
+	数据，矩阵，列表&数据框
### 格式转换&因子
+	typeof mode class
+	is.xx as.xx
+	因子：factor ordered factor
### 数据索引切片聚合
+	向量索引
	+	顺序
	+	布尔
+	数据框切片
	+	顺序
	+	条件
	+	高阶索引函数
		+	subset
		+	select
		+	filter
+	变量计算
	+	transform
	+	mutate
	+	within&ifelse
+	变量聚合
	+	group_by/smmarize
	+	aggregte
	+	tpply
	+	ddply
		+	count
		+	sum
		+	mean
		+	min/max
### 数据合并&追加&塑造
+	无匹配合并
	+	纵向合并	
		+	rbind
		+	bind_rows
	+	横向合并
		+	cbind
		+	bind_cols
+	数据连接
	+	merge 
	+	left/right/full/inner_join
	+	Data.table[X,on='key']
+	长宽转换
	+	reshape2:：melt/dcast
	+	tidyr：：gather/spread
### 字符串处理与正则
+	字符串格式化
	+ paste str_c
	+ print cat
	+ sprintf
	+ pystr
+	拆分与合并
	+	split str_split
	+	unite separate
+	字符串提取与正则表达式
	+	length
	+	substr substring
	+	grep grepl
	+	sub gsub 
### 管道函数&向量化运算
+	管道函数
	+	magrittr
	+	%>%
+	向量化函数
	+	plyr：：apply tapply sapply lapply ddply l_ply
	+	r_ply m_ply
### 非结构数据
+	jsonliste
	+	fromJSON
	+	toJSON
+	rlist
	+	list.load list.save
	+	list.map list.select list.rbind
### R与数据库交互
+	RMySQL
+	rmongodb
### 数据处理神器data.table
+	读写
	+	fread fwrite
+	切片/索引/聚合
	+	DT[i,j,by]


----------
	
## 设计基础
### 设计基础
+   字体，色彩，版式，设计元素
### 色彩
+   色相，饱和度，亮度
### 排版
+   对齐，对比，亲密性，重复
### R字体
+	showtext
+	字体导入
	+	font_add("myfont","msyh.ttc") 
	+	font_families() 
+	基础函数
+	字体导入
	+	windowsFonts( 
	    myFont = windowsFont("微软雅黑")
	     )
	+	png("myplot3.jpeg")
	+	ggplot(diamonds,aes(color,fill=cut))+
	  geom_bar()+ggtitle("钻石质量情况")+theme(title=element_text(family="myFont"))
	+	dev.off()
### R色彩
+	预设调色板
	+	rainbow
	+	heat.colors
	+	terrain.colors
	+	topo.colors
	+	cm.colors
+	自定义调色板
	+	colorRampPalette(c("red", "green"))(n)
+	灰度调色板
	+	gray(0:n/n)
+	hsv自定义调色板
	+	hsv(h = 1, s = 1, v = 1, alpha)
+	第三方扩展包
	+	RcolorBrewer
	+	ggthemes
	+	ggtech
+	library("scales")
+	show_col(sample(rainbow(1000),replace = FALSE),labels = FALSE)

----------

## ggplot2
### 地位
+	import
	+	readr
	+	httr
	+	rvest
	+	RCurl
	+	xml2
	+	jsonlite
	+	rlist
	+	RMySQL
+	Transform
	+	dplyr
	+	tidyr
	+	data.table
	+	lubridate
	+	stringr
	+	magrittr
+	Model
	+	Broom
	+	modelr
+	Visualisation
	+	ggplot2
### 理念
+	几何图层
+	坐标系转换
+	标度调整
+	分面系统
+	图例
### 框架
+   数据
    +   几何图层（统计变换）：geom_xxx()， stat_xxx()
    +   数据映射
        +   美学映射：mapping_aes(): x,y,col,color,colour,group,size,alpha,linetype
        +   位置调整：positon adjustment :identity,stack,dodge,fill
    +   坐标系转换 coordinate
        +   coord_cartesian,coord_fixed,coord_flip,coord_polar,coord_map
    +   标度调整 scales
        +   scale_x|y_xxx, scale_fill/color_xxx,scale_size_xxx
        +   scale_alpha_xxx
        +   scale_line_type_xxx
        +   scale_line_shape_xxx
    +   分面 facetting
        +   facet_grid
        +   facet_wrap
+   美化
    +   图例调整    guides
        +   guide_colourbar
        +   guide_legend
    +   主题   themes
        +   element_line
        +   element_text
        +   element_rect
        +   element_blank
    +   数据标签 geom_text()
    +   自定义注释 annotation()
    +   标题，副标题，备注 labs()
### 图层
#### mapping
+   mapping（x,y,size,alpha,linetype,colour,fill)
+   geom_bar(mapping = NULL, data = NULL, stat = "count",position = "stack)
+   stat_count(mapping = NULL, data = NULL, geom = "bar",position = "stack")
#### position
+   bar,area,histigram
+   identity ：序列相互遮盖，不做任何位置调整
+   stack:垂直堆叠，堆积柱状图
+   fill:百分比堆叠，百分不堆积面积图
+   Dodge：水平抖动放置，簇状柱状图
###   标度
+   物理元素
    +   点线面;形状大小;（shape,linetype,size)
+   色彩元素
    +   色相，颜色，透明度；
    +   分面，分组（facet，group）
    +   坐标轴设定(x,y)
+   标度调整
    +   x,y,colour,fill,alpha,scale,shape,linetype
###   坐标轴
+   coord_cartesian 笛卡尔，默认
+   coord_fixed 固定宽高比
+   coord_flip 翻转
+   coord_map 地图
+   coord_polar 极坐标
###   图例
+   guides
    +   title,title.vjust,title.hjust
    +   label,label.vjust,label.hjust,direction
    +   size:barwidth/barheight,nbin,ticks
###   标签
+	标签是：带有美学映射的几何图层
+   geom_text
+   labs
+   annotations
###   分面
+   facet_grid 网格分面
+   facet_wrap 一维分面
###  主题
+   text
+   rect
+   line

### 参数共享
+	ggplot-geom_xxx：通用的写在ggplot中；如果有不同的图形和数据源，写在对应的geom_xxx中
+	数据是否写在aes内：共性数据映射：写在aes外；个性数据映射，写在aes内；
### 几何对象和统计变化
+	geom_xxx和stat_xxx动作一致
+	每个图层：一个几何对象+一个统计变化
+	每一个geom_xxx：都包含一个stat变换
+	每一个stat_xxx：都拥有一个geom对象
+	geom_bar(mapping = NULL, data = NULL, stat = "count",position = "stack)
+	stat_count(mapping = NULL, data = NULL, geom = "bar",position = "stack")
+	ggplot(data= NULL, aes(x = x, y = y)) +  
  geom_point(color = "darkred" , stat = "identity")
+	ggplot(data= NULL, aes(x = x, y = y)) +  
stat_identity(color = "darkred" , geom = "point") 

# 常用图形
#散点图：
#使用geom_xxx几何对象构建散点图形：
ggplot(data= NULL, aes(x = x, y = y)) +  
  geom_point(color = "darkred" , stat = "identity")

#使用stat统计变换几何对象构建散点图形：
ggplot(data= NULL, aes(x = x, y = y)) +  
stat_identity(color = "darkred" , geom = "point") 

#柱形图：

x <- sample(LETTERS[1:5],size = 20,replace = TRUE )
y <- runif(20,1,50)

#频率图
ggplot(data = NULL , aes(x =x)) +
  geom_bar(stat = "count")

ggplot(data = NULL , aes(x =x)) +
stat_count(geom = "bar")

#类别求和：

ggplot(data = NULL , aes(x =x , y = y)) +
  geom_bar(stat = "identity")

ggplot(data = NULL , aes(x =x , y = y)) +
  geom_bar(stat = "sum")

ggplot(data = NULL , aes(x =x , y = y)) +
  geom_col()  

###4、位置调整参数（position）:
###位置参数调整：

data<-data.frame(
  Conpany = c("Apple","Google","Facebook","Amozon","Tencent"),
  Sale2015 = c(5000,3500,2300,2100,3100),
  Sale2016 = c(5050,3800,2900,2500,3300))

library(reshape2)

mydata <- melt(data,id.vars="Conpany",variable.name="Year",value.name="Sale")	

#多序列保持不变：
ggplot(mydata,aes(Conpany,Sale,fill=Year))+
  geom_bar(stat="identity",position="identity",alpha=.5)
#多序列簇状柱形图：		 
ggplot(mydata,aes(Conpany,Sale,fill=Year))+
  geom_bar(stat="identity",position="dodge")
#多序列堆积柱形图：		 
ggplot(mydata,aes(Conpany,Sale,fill=Year))+
  geom_bar(stat="identity",position="stack")
#多序列百分比堆积柱形图：		 
ggplot(mydata,aes(Conpany,Sale,fill=Year))+
  geom_bar(stat="identity",position="fill")


###3.6 分面系统：

###分面案例：
data<-data.frame(Name = c("苹果","谷歌","脸书","亚马逊","腾讯"),Conpany = c("Apple","Google","Facebook","Amozon","Tencent"),Sale2013 = c(5000,3500,2300,2100,3100),Sale2014 = c(5050,3800,2900,2500,3300),Sale2015 = c(5050,3800,2900,2500,3300),Sale2016 = c(5050,3800,2900,2500,3300))
mydata<-melt(data,id.vars=c("Name","Conpany"),variable.name="Year",value.name="Sale")

ggplot(mydata,aes(reorder(Conpany,-Sale),Sale,fill=Year))+
  geom_bar(stat="identity",position="dodge")


###按列分面
ggplot(mydata,aes(reorder(Conpany,-Sale),Sale,fill=Year))+
  geom_bar(stat="identity",position="dodge")+
  facet_grid(.~Year)   

###按行分面
ggplot(mydata,aes(reorder(Conpany,-Sale),Sale,fill=Year))+
  geom_bar(stat="identity",position="dodge")+
  facet_grid(Year~.)   

###使用封装分面
ggplot(mydata,aes(reorder(Conpany,-Sale),Sale,fill=Year))+
  geom_bar(stat="identity",position="dodge")+
  facet_wrap(~Year) 
----------

## 标度&图例&坐标系&主题
### xy轴标度
+	scale_x
### 颜色标度
+	scale_alpha
### 图例
+	guides
### 坐标轴系统
+	coord_flip
+	coord_map
+	coord_polar
### 主题与自定义
+	text
+	rect
+	line
# 图形

########4.1 x/y轴标度详解###############

library("ggplot2")
mydata1 <- data.frame(
  x = 1:100,
  y = rnorm(100,1000,500)
)

#三种常见的坐标轴变换

p1 <- ggplot(mydata1, aes(x, y)) +
  geom_point();p1


p1 + scale_y_continuous(trans = "log10")
p1 + scale_y_log10()

p1 + scale_y_continuous(trans = "sqrt")
p1 + scale_y_sqrt()

p1 +scale_y_reverse()
#p1 +scale_x_reverse()
p1 +scale_y_continuous(trans = "reverse")
#p1 +scale_x_continuous(trans = "reverse")



#连续型坐标轴/离散型坐标轴标度函数中的主要参数：

#连续型坐标轴

p1 <- ggplot(mydata1, aes(x, y)) + geom_point();p1


p1 + scale_x_continuous(                #离散坐标轴（ggplot函数会通过探知x轴对应的变量格式来自动分配对应的默认标度类型，
                                        #如需修改一定要确保你使用的标度函数与坐标轴对应变量类型一致）
  name = "X轴",                         #坐标轴轴标题（与labs函数中的x='',y=''标题函数一致，仅需设置一个即可）
  limits = c(25,75),                    #坐标轴指标刻度范围（默认情况下会显示完整的极差范围【最小值~最大值】,这里可以自定义，但是会丢弃部分记录）
  breaks = seq(25,75,5),                #刻度线间隔点（默认情况下会根据坐标轴所依赖的指标极差自适应计算最佳刻度线间隔点，可以自定义）
  minor_breaks = seq(seq(25,75,2.5)),   #次刻度线间隔点；
  labels = c(paste0(seq(25,75,5),'个')),#坐标轴刻度标签（默认情况下，根据主刻度线间隔点中处的数值自动生成标签，可自定义为任何格式）
  expand = c(0,0),                      #坐标轴刻度线起始位置与绘图区间隔距离，默认情况下连续型：c(0.05,0)离散型坐标轴：c(0, 0.6)
  position = "top"
)


#连续型坐标轴连续型坐标轴——日期时间型

lct <- Sys.getlocale("LC_TIME")
Sys.setlocale("LC_TIME", "C")


library("ggplot2")
mydata1 <- data.frame(
  x = seq(as.Date('2018-03-01'),as.Date('2018-03-31'),by = '1 day'),
  y = rnorm(31,1000,500)
)

p1 <- ggplot(mydata1, aes(x, y)) + geom_line();p1

p1 + scale_x_date(
  limits = c(Sys.Date() - 15, Sys.Date())
  )   #limits仍然可以用于限制轴标度范围



#预定义刻度刻度线间隔区间与刻度标签
p1 + scale_x_date(date_labels = "%b %d")                     #输出刻度线标签为：短月份 两位日期 
p1 + scale_x_date(date_breaks = "1 week")                    #刻度线间隔区间为一周
p1 + scale_x_date(date_breaks = "1 week", date_labels = "%W")#刻度线间隔为一周，刻度标签显示格式为月份
p1 + scale_x_date(date_minor_breaks = "1 day")

#自定义刻度刻度线间隔区间与刻度标签
p1 + scale_x_date(
  breaks = seq(as.Date('2018-03-01'),as.Date('2018-03-31'),by = '3 days'),
  labels = format(seq(as.Date('2018-03-01'),as.Date('2018-03-31'),by = '3 days'),format = "%m/%d")
  )   

 
Sys.setlocale("LC_TIME", lct)   #恢复本地时期时间显示格式

#离散坐标轴标度调整

mydata2 <- data.frame(
  x = sample(LETTERS[1:5],20,replace = TRUE),
  y = runif(20,100,500)
)


p1 <- ggplot(mydata2, aes(x, y)) + geom_bar(stat = "identity");p1

p1 + scale_x_discrete(
  name = "X轴",                       #坐标轴轴标题（与labs函数中的x='',y=''标题函数一致，仅需设置一个即可）
  limits = c("A","B","C","D"),        #坐标轴显示类别范围（默认情况下会显示离散变量的所有子类,这里可以自定义要显示的类别范围，未涵盖范围会被丢弃）
  breaks = c("C","D"),                #刻度线间隔点（默认情况下会根据坐标轴所依赖的指标极差自适应计算最佳刻度线间隔点，可以自定义）
  labels = paste0(c("C","D"),'箱'),   #坐标轴刻度标签（默认情况下，根据主刻度线间隔点中处的数值自动生成标签，可自定义为任何格式）
  expand = c(0,0),                    #坐标轴刻度线起始位置与绘图区间隔距离，默认情况下连续型：c(0.05,0)离散型坐标轴：c(0, 0.6)
  position = "top"
)

########4.2 颜色标度详解###############

#颜色标度之透明度标度

#连续变量透明度标度
diamonds1 <- diamonds[sample(nrow(diamonds),1000),]

p <- ggplot(diamonds1, aes(depth, price)) +
  geom_point(aes(alpha = carat));p
p + scale_alpha_continuous(range = c(0.4, 0.8))


#离散变量透明度标度
p <- ggplot(diamonds1, aes(depth, price)) +
  geom_point(aes(alpha = color));p
p + scale_alpha_discrete(range = c(0.4, 0.8))

#离散变量透明度标度的自定义形式

#> levels(diamonds$color)
#[1] "D" "E" "F" "G" "H" "I" "J"
p <- ggplot(diamonds1, aes(depth, price)) +
  geom_point(aes(alpha = color));p

p + scale_alpha_manual(
  limits = levels(diamonds$color),              
  breaks =  c("D","E","F","G","H"),
  labels = c("D-d","E-e","F-f","G-g","H-h"),
  values = c(0.15,0.2,0.3,0.4,0.5,0.6,0.75)
  )


####4.2 颜色标度详解——填充色、轮廓色标度####


#连续型颜色标度

mydata3 <- data.frame(
  x = runif(100,0,100),
  y = runif(100,0,100),
  z = runif(100,0,100),
  f = runif(100,0,100),
  g = rep(LETTERS[1:5],each = 20)
)

p <- ggplot(mydata3, aes(x, y)) +
  geom_point(aes(colour = z), shape = 19,size= 5);p

#scale_colour_gradient()——双色过渡渐变

p + scale_colour_continuous(
  low = "#FEE0B6", 
  high = "#006837",
  guide = "colorbar"
  )

p + scale_colour_gradient(
  low = "#FEE0B6", 
  high = "#006837",
  guide = "colorbar"
)


#scale_colour_gradient2()——三色过渡渐变

p + scale_colour_gradient2(
  low = "#1A9850", 
  mid = "#F5F5F5",
  high = "#F46D43",
  guide = "colorbar",
  midpoint = mean(mydata3$z)
)

p + scale_colour_gradient2(
  low = "#1A9850", 
  mid = "#F5F5F5",
  high = "#F46D43",
  guide = "colorbar"
)


#离散色盘渐变化scale_colour/fill_distiller()

p + scale_colour_distiller(
  type = "seq",
  palette = 1,
  direction = 1
)

p + scale_colour_distiller(palette= "RdYlBu")
p + scale_colour_distiller(palette= "RdYlGn")


#离散渐变颜色标度调整函数

p <- ggplot(mydata3, aes(x, y)) +
  geom_point(aes(colour = g), shape = 19,size= 5);p

p + scale_colour_discrete()
p + scale_colour_hue()      #等价于scale_colour_discrete

p + scale_colour_grey()

# 离散渐变的成熟配色方案

#scale_colour/fill_brewer

p <- ggplot(mydata3, aes(x, y)) +
  geom_point(aes(colour = g), shape = 19,size= 5);p

#单色系
p + scale_colour_brewer(type = "seq", palette = 1, direction = -1)
p + scale_colour_brewer(palette = "Blues", direction = -1)
p + scale_colour_brewer(palette = "Greens", direction = -1)
p + scale_colour_brewer(palette = "Reds", direction = -1)

#二分色系
p + scale_colour_brewer(palette = "RdYlBu", direction = -1)
p + scale_colour_brewer(palette = "RdYlGn", direction = -1)

#分类色系
p + scale_colour_brewer(palette = "Accent", direction = -1)
p + scale_colour_brewer(palette = "Paired", direction = -1)
 

#自定义色盘

p <- ggplot(mydata3, aes(x, y)) +
  geom_point(aes(colour = g), shape = 19,size= 5);p

p + scale_colour_manual(
  limits = LETTERS[1:4],
  #breaks = LETTERS[1:4],
  labels = c("A_a","B_b","C_c","D_d"),
  values = c("#F46D43","#D9F0D3","#1A9850","#006837")
)

p + scale_colour_manual(
  limits = LETTERS[1:4],
  breaks = LETTERS[4:1],
  labels = c("A_a","B_b","C_c","D_d"),
  values = c("#F46D43","#D9F0D3","#1A9850","#006837")
)

unique(mydata3$g)
#[1] A B C D E
#Levels: A B C D E

#####4.3 其他标度(大小、形状、线条)详解####

##linetype——线形状
lct <- Sys.getlocale("LC_TIME")
Sys.setlocale("LC_TIME", "C")

mydata4 <- data.frame(
  x = rep(seq(as.Date('2018-03-01'),as.Date('2018-03-10'),by = '1 day'),each = 5),
  y = abs(rnorm(50,1000,500)),
  z = rep(LETTERS[1:5],length = 50)
)

p <- ggplot(mydata4,aes(x,y)) +
  geom_line(aes(linetype = z,colour = z),size = 1.5);p

p + scale_linetype_discrete()

#p + scale_linetype_continuous()   #错误

p + scale_linetype_manual(
  limits = LETTERS[1:5],
  breaks = LETTERS[1:5],
  labels = paste0(LETTERS[1:5],'_',letters[1:5]),
  values = c('solid','dashed','dotted','dotdash','longdash')
  )


##shape——点形状

p <- ggplot(mydata4,aes(x,y,colour = z)) +
  geom_line(size = 1.5) +
  geom_point(aes(,shape = z),size =  5);p 

p + scale_shape_discrete()

p + scale_shape_continuous()

p +scale_shape_manual(
  limits = LETTERS[1:5],
  breaks = LETTERS[1:5],
  labels = paste0(LETTERS[1:5],'_',letters[1:5]),
  values = c(0,1,2,5,6)
 )

###点大小

mydata6 <- data.frame(
  x = runif(100,1,100),
  y = runif(100,1,100),
  z = runif(100,1,100)
)

p <- ggplot(mydata6,aes(x,y,size = z)) +
  geom_point();p


p + scale_radius()
p + scale_size()

p + scale_size_discrete()


p + scale_size_area(
  limits = c(20,80),
  breaks = seq(20,80,5),
  labels = paste(seq(20,80,5),'$')
)


#共享继承关系

p <- ggplot(mydata4,aes(x,y,group = z)) +
  geom_line(size = 1.5) +
  geom_point(aes(shape = z),size =  5);p

ggplot() +
  geom_line(mydata4,aes(x,y,group = z),size = 1.5) +
  geom_point(mydata4,aes(x,y,shape = z),size =  5)


p + scale_shape_manual(
    limits = LETTERS[1:5],
    values = c(0,1,2,5,6)
  )

#美学映射与分组参数

p <- ggplot(mydata4,aes(x,y,colour = z)) +
  geom_line(size = 1.5);p
p +  geom_point(aes(shape = z),size =  5) +
  scale_shape_manual(
    limits = LETTERS[1:5],
    values = c(0,1,2,5,6)
  )


Sys.setlocale("LC_TIME", lct)

####4.4 图例系统详解####

guides(
  fill/color = guide_legend(...),
  guide_colorbar(...)
  )

###连续型颜色图例：
guide_colourbar(
  title=waiver(), 
  title.position=NULL,
  title.theme=NULL, 
  title.hjust=NULL,
  title.vjust = NULL,
  label=TRUE,
  label.position=NULL,
  label.theme = NULL,
  label.hjust = NULL, 
  label.vjust = NULL, 
  barwidth =NULL,
  barheight = NULL, 
  nbin = 20,
  ticks=TRUE,
  draw.ulim=TRUE, 
  draw.llim = TRUE, 
  direction = NULL,
  default.unit="line",
  reverse=FALSE,
  order=0,...
)

###离散型图例函数
guide=guide_legend(
  
  title=NULL,
  title.position="left",
  title.theme=element_text(size=15,face="italic",colour="red",angle=45),
  keywidth=3,
  keyheight=1,
  label.position="bottom",
  direction="horizontal",
  label.hjust=0.5,
  label.vjust=0.5,
  label.theme=element_text(size=15,face="italic",colour="red",angle=45),override.aes=list(alpha=1)),
  nrow=8,
  ncol=8,
  byrow=TRUE,
  reverse = TRUE
)


mydata5 <- data.frame(
  x = runif(100,0,100),
  y = runif(100,0,100),
  z = runif(100,0,100),
  f = runif(100,0,100),
  g = rep(LETTERS[1:5],each = 20)
)

p <- ggplot(mydata5,aes(x,y))+
  geom_point(aes(fill = z,size = f ),shape = 21);p


colorbar = guide_colorbar(
  title = 'Colorbar',
  title.position = 'left',
  #left,right,top,bottom
  title.theme = element_text(size = 15,face = "italic",colour = "red",angle = 45),
  title.hjust =  .5,
  title.vjust =  0,
  label = TRUE,
  label.position = 'top',
  label.theme = element_text(size = 15,face = "italic",colour = "red",angle = 45),
  label.hjust = .5,
  label.vjust = .5,
  barwidth = unit(6,"cm"),
  #Default value is legend.key.width or legend.key.siz
  barheight = unit(1.2,"cm"),
  #Default value is legend.key.height or legend.key.size
  nbin = 20,
  ticks = TRUE,
  draw.ulim = TRUE,
  draw.llim = TRUE,
  direction = "horizontal",
  #"horizontal" or "vertical."
  reverse = TRUE,
  order = 1
)


size_legend = guide_legend(
  title = 'legend',
  title.position = "left",
  title.hjust =  .5,
  title.vjust = .5,
  title.theme = element_text(size = 15,face = "italic",colour = "red",angle = 45),
  keywidth = 2.5,
  keyheight = 2,
  label.position = "bottom",
  direction = "horizontal",
  label = TRUE,
  label.hjust = 0.5,
  label.vjust = 0.5,
  label.theme = element_text(size = 15,face = "italic",colour = "red",angle = 45),
  nrow = 2,
  byrow = TRUE,
  reverse = TRUE,
  order = 2
)


p + scale_fill_gradient(breaks = seq(0,100,10)) +
  scale_size_area(breaks = seq(0,100,10))  +
  guides(fill = colorbar,size = size_legend)


####4.5 坐标轴系统####

#笛卡尔坐标系翻转：
library("magrittr")
library("reshape2")
library("ggplot2")

mydata <- data.frame(
  Name = c("苹果","谷歌","脸书","亚马逊","腾讯"),
  Company = c("Apple","Google","Facebook","Amozon","Tencent"),
  Sale2013 = c(5000,3500,2300,2100,3100),
  Sale2014 = c(5050,3800,2900,2500,3300),
  Sale2015 = c(5050,3800,2900,2500,3300),
  Sale2016 = c(5050,3800,2900,2500,3300)
  )  %>% melt(id.vars=c("Company","Name"),variable.name="Year",value.name="Sale")

#单序列翻转
ggplot(mydata[mydata$Year == 'Sale2016',],aes(Company,Sale,fill = Company))+
  geom_bar(stat="identity") +
  coord_flip(expand = FALSE) 

#多序列翻转(簇状柱形图)
ggplot(mydata,aes(Company,Sale,fill=Year)) +
  geom_bar(stat="identity",position="dodge") +
  coord_flip(expand = FALSE)

#多序列翻转（堆积柱形图）
ggplot(mydata,aes(Company,Sale,fill=Year))+
  geom_bar(stat="identity",position="stack")+
  coord_flip(expand = FALSE)

#笛卡尔坐标系与极坐标系互转：

#将Y轴绕着X轴旋转一个圆周

ggplot(diamonds,aes(x=1,fill=cut)) +
  geom_bar(width=1) +
  coord_polar(
    theta = "y", 
    start = 0, 
    direction = 1
    )

#将X轴绕着Y轴旋转一个圆周

ggplot(diamonds,aes(x=1,fill=cut))+
  geom_bar(width=1)+
  scale_x_discrete(expand = c(0,0)) +
  coord_polar(
    theta = "x", 
    start = 0, 
    direction = 1
  )

#单序列柱形图沿着Y轴宣传360度——条环图

ggplot(diamonds,aes(cut))+
  geom_bar(width=1,fill="steelblue",colour="white") +
  coord_polar(theta = "y",start=0)

#单序列柱形图沿着x轴宣传360度——玫瑰图

ggplot(diamonds,aes(cut))+
  geom_bar(width=1,fill="#3182BD")+
  coord_polar(theta = "x",start=0)


#簇状/堆积柱形图
#沿着X轴旋转

ggplot(diamonds,aes(x=color,fill=cut))+
  geom_bar(width=0.95,colour="white",position = 'dodge') +
  coord_polar(theta = "x",start=0)

ggplot(diamonds,aes(x=color,fill=cut))+
  geom_bar(width=0.95,colour="white",position = 'stack') +
  coord_polar(theta = "x",start=0)

#沿着Y轴旋转

ggplot(diamonds,aes(x=color,fill=cut))+
  geom_bar(width=0.95,colour="white",position = 'dodge') +
  coord_polar(theta = "y",start=0)

ggplot(diamonds,aes(x=color,fill=cut))+
  geom_bar(width=0.95,colour="white",position = 'stack') +
  coord_polar(theta = "y",start=0)


####地理信息坐标系

library("maps")  
library("plyr")    
library("mapdata") 

world_map <- map_data("world")   #美国地图数据：

ggplot(world_map, aes(x=long,y=lat,group=group)) +
  geom_path(colour = "grey") +
  labs(title = "World Map")     


ggplot(world_map,aes(x=long,y=lat,group = group))+
  geom_polygon(aes(fill = region),colour="black")+
  labs(title = "World Map") +
  guides(fill = FALSE)


ggplot(world_map,aes(x=long,y=lat,group=group))+
  geom_polygon(aes(fill=region),colour="black")+
  labs(title = "World Map") +
  guides(fill = FALSE) +
  coord_map("ortho",orientation=c(0,0,0)) 


####4.6 主题封装与自定义####

library("ggplot2")
library("reshape2")
library("ggthemes")
library("magrittr")

mydata <- data.frame(
  Name = c("苹果","谷歌","脸书","亚马逊","腾讯"),
  Company = c("Apple","Google","Facebook","Amozon","Tencent"),
  Sale2013 = c(5000,3500,2300,2100,3100),
  Sale2014 = c(5050,3800,2900,2500,3300),
  Sale2015 = c(5050,3800,2900,2500,3300),
  Sale2016 = c(5050,3800,2900,2500,3300)
  )  %>% melt(
  id.vars=c("Name","Company"),
  variable.name="Year",
  value.name="Sale"
  )

#默认主题
ggplot(mydata,aes(Company,Sale,fill=Year))+
  geom_bar(stat="identity")

#默认主题（theme_gray()）
ggplot(mydata,aes(Company,Sale,fill=Year))+
  geom_bar(stat="identity")+
  theme_gray()


#预设主题1
windowsFonts( myFont = windowsFont("微软雅黑"))

ggplot(mydata,aes(Company,Sale,fill=Year))+
  geom_bar(stat="identity")

theme_gray()
theme_bw()

###方法一：

theme_xmf <- theme_replace(
  plot.title       =  element_text(size = 20,family="myFont",hjust = 0,lineheight = 2),
  plot.subtitle    =  element_text(size = 15,family="myFont",hjust = 0,lineheight = 2),
  plot.caption     =  element_text(size = 18,family="myFont",hjust = 0,lineheight = 2),
  plot.background  =  element_rect( fill = '#efefef',size = 0.8 ,linetype = 3, color = 'grey'),
  plot.margin      =  margin(10,5,10,5,unit="pt"),
  legend.position  =  "top" ,
  panel.border     =  element_blank(),
  panel.background =  element_rect(fill = '#d4dee7',size = 2 ,linetype = 3, color = 'grey'),
  panel.grid.major =  element_line(linetype = "dashed"),
  panel.grid.minor =  element_blank(),
  axis.line        =  element_line(size = 1.2 , colour = 'black',linetype  = 1),
  axis.text        =  element_text(size=10,colour="#003087",family="myFont"),
  legend.text      =  element_text(size=9,colour="#003087",family="myFont"),
  legend.key       =  element_blank()
)

ggplot(mydata,aes(Company,Sale,fill=Year))+
  geom_bar(stat="identity") +
  scale_fill_brewer(palette="Blues") +
  guides(fill = guide_legend(reverse = TRUE)) +
  labs(
    title = '这里是主标题',
    subtitle = '这里是副标题',
    caption = '这里是备注'
  ) +  theme_xmf

###方法2

theme_manual <- function(){
  theme_get() %+replace% theme(
    plot.title      = element_text(size = 20,family="myFont",hjust = 0,lineheight = 2),
    plot.subtitle   = element_text(size = 15,family="myFont",hjust = 0,lineheight = 2),
    plot.caption    = element_text(size = 18,family="myFont",hjust = 0,lineheight = 2),
    plot.background = element_rect(fill = '#efefef',size = 0.8 ,linetype = 3, color = 'grey'),
    plot.margin     = margin(10,5,10,5,unit="pt"),
    legend.position="top",
    panel.border=element_blank(),
    panel.background = element_rect(fill = '#d4dee7',size = 2 ,linetype = 3, color = 'grey'),
    panel.grid.major=element_line(linetype="dashed"),
    panel.grid.minor=element_blank(),
    axis.line = element_line(size = 1.2 , colour = 'black',linetype  = 1),
    axis.text=element_text(size=10,colour="#003087",family="myFont"),
    legend.text=element_text(size=9,colour="#003087",family="myFont"),
    legend.key=element_blank()
  )
} 

ggplot(mydata,aes(Company,Sale,fill=Year))+
  geom_bar(stat="identity") +
  scale_fill_brewer(palette="Blues") +
  guides(fill = guide_legend(reverse = TRUE)) +
  labs(
    title = '这里是主标题',
    subtitle = '这里是副标题',
    caption = '这里是备注'
  ) + theme_manual()


----------
## 配色系统
### 基础配色
+	scale_fill_manual
### ggplot配色
### RcolorBrewer配色
### ggthemes主题包
### 其他配色
+	ggtech
+	ggthemer
+	ggsci

----------
## 笛卡尔坐标系
## 极坐标系应用
## 辅助几何对象
## 空间可视化
## 信息图与空间可视化
## 图形输出&精准控制