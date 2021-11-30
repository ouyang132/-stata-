# -stata-
本代码来源于自己学习和结合中国工业经济期刊中-------信息基础设施建设对企业劳动力需求的影响：需求规模、结构变化及影响路径
#在开始前我们需要下载几个命令
findit ivreghdfe
findit ivreg2
ssc install ranktest
[注意]4和5的安装是为了安装 ivreghdfe命令，不然其无法运行
findit reghdfe

--------------------------------------------------
安装命令结束
---------------------------------------------------
导入数据----可在中国工业经济期刊官网上下载
----------------------------------------
开始第文献中第一个表格
-------------------------------------
global var1 "lnage top10 lnshareholder boarder"      #创建全局暂元-----即控制变量（企业层面）
global var2 "lngdppc lnpop second third lncollstu lnroad"     #城市层面
reghdfe lnlabor station_p $var1 $var2,absorb(id dg2#year) cluster（dp4）     #reghdfe多维面板固定效应估计    【语法】reghdfe depvar [indepvars] [if] [in] [weight], absorb(absvars) [options]
#absorb（） 可以引入多维固定效应 absorb（var1,var2,...）  也可以引入交互项，absorb（var1#var2）   此处id指企业，dg#year 省份和年份交互项  cluster表示城市之间的无相关性
est store m1    #保存为m1
ivreghdfe lnlabor (station_p=iv1) $var1 $var2, absorb(id dq2#year) cluster(dq4) first
est store m2

ivreghdfe lnlabor (station_p=iv2) $var1 $var2, absorb(id dq2#year) cluster(dq4) first   #工具变量法中第一阶段，用以估计工具变量系数，first可以将两阶段都显示
est store m3

ivreghdfe lnlabor (station_p=iv1 iv2) $var1 $var2, absorb(id dq2#year) cluster(dq4) first
est store m4

reghdfe lnlabor iv1 iv2 $var1 $var2, absorb(id dq2#year) cluster(dq4)
est store m5
reghdfe lnlabor station_p iv1 iv2 $var1 $var2, absorb(id dq2#year) cluster(dq4)
est store m6
#整理成结果 代码就不展示
 --------------------------------------------------
 第二张表   信息基础建设与劳动力结构
-----------------------------------------------------
reghdfe lnhigh_edu station_p $var1 $var2, absorb(id dq2#year) cluster(dq4)
保存表格的代码也将不在展示
reghdfe lnhigh_edu (station_p=iv1 iv2) $var1 $var2,absorb(id dq2#year) cluster(dq4)
reghdfe lnlow_edu station_p $var1 $var2, absorb(id dq2#year) cluster(dq4)
----------------------------------------------------------------
表三  劳动力岗位结构
----------------------------------------------------------------
reghdfe lnoccp1 station_p $var1 $var2, absorb(id dq2#year) cluster(dq4)
reghdfe lnoccp2 station_p $var1 $var2, absorb(id dq2#year) cluster(dq4)

reghdfe lnoccp3 station_p $var1 $var2, absorb(id dq2#year) cluster(dq4)

reghdfe lnoccp4 station_p $var1 $var2, absorb(id dq2#year) cluster(dq4)

reghdfe lnoccp5 station_p $var1 $var2, absorb(id dq2#year) cluster(dq4)

reghdfe lnoccp67 station_p $var1 $var2, absorb(id dq2#year) cluster(dq4)

reghdfe lnoccp8 station_p $var1 $var2, absorb(id dq2#year) cluster(dq4)
reghdfe lnoccp9 station_p $var1 $var2, absorb(id dq2#year) cluster(dq4)
ivreghdfe lnoccp1 (station_p=iv1 iv2) $var1 $var2, absorb(id dq2#year) cluster(dq4)

ivreghdfe lnoccp2 (station_p=iv1 iv2) $var1 $var2, absorb(id dq2#year) cluster(dq4)

ivreghdfe lnoccp3 (station_p=iv1 iv2) $var1 $var2, absorb(id dq2#year) cluster(dq4)

ivreghdfe lnoccp4 (station_p=iv1 iv2) $var1 $var2, absorb(id dq2#year) cluster(dq4)

ivreghdfe lnoccp5 (station_p=iv1 iv2) $var1 $var2, absorb(id dq2#year) cluster(dq4)

ivreghdfe lnoccp67 (station_p=iv1 iv2) $var1 $var2, absorb(id dq2#year) cluster(dq4)
est store m6
ivreghdfe lnoccp8 (station_p=iv1 iv2) $var1 $var2, absorb(id dq2#year) cluster(dq4)

ivreghdfe lnoccp9_11 (station_p=iv1 iv2) $var1 $var2, absorb(id dq2#year) cluster(dq4)
-------------------------------------------------------------------
异质性性分析
-------------------------------------------------------------------



#在画图前需要先回归
ivreghdfe lnlabor (station_p=iv1 iv2) $var1 $var2 if state==1, absorb(id dq2#year) cluster(dq4)
est store m1
ivreghdfe lnhigh_edu (station_p=iv1 iv2) $var1 $var2 if state==1, absorb(id dq2#year) cluster(dq4)
est store m2
ivreghdfe lnlow_edu (station_p=iv1 iv2) $var1 $var2 if state==1, absorb(id dq2#year) cluster(dq4)
est store m3

ivreghdfe lnoccp1 (station_p=iv1 iv2) $var1 $var2 if state==1, absorb(id dq2#year) cluster(dq4)
est store m4
ivreghdfe lnoccp2 (station_p=iv1 iv2) $var1 $var2 if state==1, absorb(id dq2#year) cluster(dq4)
est store m5
ivreghdfe lnoccp3 (station_p=iv1 iv2) $var1 $var2 if state==1, absorb(id dq2#year) cluster(dq4)
est store m6
ivreghdfe lnoccp4 (station_p=iv1 iv2) $var1 $var2 if state==1, absorb(id dq2#year) cluster(dq4)
est store m7
ivreghdfe lnoccp5 (station_p=iv1 iv2) $var1 $var2 if state==1, absorb(id dq2#year) cluster(dq4)
est store m8
ivreghdfe lnoccp67 (station_p=iv1 iv2) $var1 $var2 if state==1, absorb(id dq2#year) cluster(dq4)
est store m9
ivreghdfe lnoccp8 (station_p=iv1 iv2) $var1 $var2 if state==1, absorb(id dq2#year) cluster(dq4)
est store m10
ivreghdfe lnoccp9_11 (station_p=iv1 iv2) $var1 $var2 if state==1, absorb(id dq2#year) cluster(dq4)
est store m11
这两张图可以在excel上画出 -------------------------------------------------
通信及其上下游
-------------------------------------------------------------------------
reghdfe lnlabor station_p $var1 $var2 if info_ind==1, absorb(id dq2#year) cluster(dq4)
est store m1
reghdfe lnhigh_edu station_p $var1 $var2 if info_ind==1, absorb(id dq2#year) cluster(dq4)
est store m2
reghdfe lnlow_edu station_p $var1 $var2 if info_ind==1, absorb(id dq2#year) cluster(dq4)
est store m3
reghdfe lnoccp1 station_p $var1 $var2 if info_ind==1, absorb(id dq2#year) cluster(dq4)
est store m4
reghdfe lnoccp2 station_p $var1 $var2 if info_ind==1, absorb(id dq2#year) cluster(dq4)
est store m5
reghdfe lnoccp3 station_p $var1 $var2 if info_ind==1, absorb(id dq2#year) cluster(dq4)
est store m6
reghdfe lnoccp4 station_p $var1 $var2 if info_ind==1, absorb(id dq2#year) cluster(dq4)
est store m7
reghdfe lnoccp5 station_p $var1 $var2 if info_ind==1, absorb(id dq2#year) cluster(dq4)
est store m8
reghdfe lnoccp67 station_p $var1 $var2 if info_ind==1, absorb(id dq2#year) cluster(dq4)
est store m9
reghdfe lnoccp8 station_p $var1 $var2 if info_ind==1, absorb(id dq2#year) cluster(dq4)
est store m10
reghdfe lnoccp9_11 station_p $var1 $var2 if info_ind==1, absorb(id dq2#year) cluster(dq4)
est store m11

ivreghdfe lnlabor (station_p=iv1 iv2) $var1 $var2 if info_ind==1, absorb(id dq2#year) cluster(dq4)
est store m1
ivreghdfe lnhigh_edu (station_p=iv1 iv2) $var1 $var2 if info_ind==1, absorb(id dq2#year) cluster(dq4)
est store m2
ivreghdfe lnlow_edu (station_p=iv1 iv2) $var1 $var2 if info_ind==1, absorb(id dq2#year) cluster(dq4)
est store m3
ivreghdfe lnoccp1 (station_p=iv1 iv2) $var1 $var2 if info_ind==1, absorb(id dq2#year) cluster(dq4)
est store m4
ivreghdfe lnoccp2 (station_p=iv1 iv2) $var1 $var2 if info_ind==1, absorb(id dq2#year) cluster(dq4)
est store m5
ivreghdfe lnoccp3 (station_p=iv1 iv2) $var1 $var2 if info_ind==1, absorb(id dq2#year) cluster(dq4)
est store m6
ivreghdfe lnoccp4 (station_p=iv1 iv2) $var1 $var2 if info_ind==1, absorb(id dq2#year) cluster(dq4)
est store m7
ivreghdfe lnoccp5 (station_p=iv1 iv2) $var1 $var2 if info_ind==1, absorb(id dq2#year) cluster(dq4)
est store m8
ivreghdfe lnoccp67 (station_p=iv1 iv2) $var1 $var2 if info_ind==1, absorb(id dq2#year) cluster(dq4)
est store m9
ivreghdfe lnoccp8 (station_p=iv1 iv2) $var1 $var2 if info_ind==1, absorb(id dq2#year) cluster(dq4)
est store m10
ivreghdfe lnoccp9_11 (station_p=iv1 iv2) $var1 $var2 if info_ind==1, absorb(id dq2#year) cluster(dq4)
est store m11

reghdfe lnlabor station_p $var1 $var2 if up_ind==1, absorb(id dq2#year) cluster(dq4)
est store m1
reghdfe lnhigh_edu station_p $var1 $var2 if up_ind==1, absorb(id dq2#year) cluster(dq4)
est store m2
reghdfe lnlow_edu station_p $var1 $var2 if up_ind==1, absorb(id dq2#year) cluster(dq4)
est store m3
reghdfe lnoccp1 station_p $var1 $var2 if up_ind==1, absorb(id dq2#year) cluster(dq4)
est store m4
reghdfe lnoccp2 station_p $var1 $var2 if up_ind==1, absorb(id dq2#year) cluster(dq4)
est store m5
reghdfe lnoccp3 station_p $var1 $var2 if up_ind==1, absorb(id dq2#year) cluster(dq4)
est store m6
reghdfe lnoccp4 station_p $var1 $var2 if up_ind==1, absorb(id dq2#year) cluster(dq4)
est store m7
reghdfe lnoccp5 station_p $var1 $var2 if up_ind==1, absorb(id dq2#year) cluster(dq4)
est store m8
reghdfe lnoccp67 station_p $var1 $var2 if up_ind==1, absorb(id dq2#year) cluster(dq4)
est store m9
reghdfe lnoccp8 station_p $var1 $var2 if up_ind==1, absorb(id dq2#year) cluster(dq4)
est store m10
reghdfe lnoccp9_11 station_p $var1 $var2 if up_ind==1, absorb(id dq2#year) cluster(dq4)
est store m11

ivreghdfe lnlabor (station_p=iv1 iv2) $var1 $var2 if up_ind==1, absorb(id dq2#year) cluster(dq4)
est store m1
ivreghdfe lnhigh_edu (station_p=iv1 iv2) $var1 $var2 if up_ind==1, absorb(id dq2#year) cluster(dq4)
est store m2
ivreghdfe lnlow_edu (station_p=iv1 iv2) $var1 $var2 if up_ind==1, absorb(id dq2#year) cluster(dq4)
est store m3
ivreghdfe lnoccp1 (station_p=iv1 iv2) $var1 $var2 if up_ind==1, absorb(id dq2#year) cluster(dq4)
est store m4
ivreghdfe lnoccp2 (station_p=iv1 iv2) $var1 $var2 if up_ind==1, absorb(id dq2#year) cluster(dq4)
est store m5
ivreghdfe lnoccp3 (station_p=iv1 iv2) $var1 $var2 if up_ind==1, absorb(id dq2#year) cluster(dq4)
est store m6
ivreghdfe lnoccp4 (station_p=iv1 iv2) $var1 $var2 if up_ind==1, absorb(id dq2#year) cluster(dq4)
est store m7
ivreghdfe lnoccp5 (station_p=iv1 iv2) $var1 $var2 if up_ind==1, absorb(id dq2#year) cluster(dq4)
est store m8
ivreghdfe lnoccp67 (station_p=iv1 iv2) $var1 $var2 if up_ind==1, absorb(id dq2#year) cluster(dq4)
est store m9
ivreghdfe lnoccp8 (station_p=iv1 iv2) $var1 $var2 if up_ind==1, absorb(id dq2#year) cluster(dq4)
est store m10
ivreghdfe lnoccp9_11 (station_p=iv1 iv2) $var1 $var2 if up_ind==1, absorb(id dq2#year) cluster(dq4)
est store m11

reghdfe lnlabor station_p $var1 $var2 if down_ind==1, absorb(id dq2#year) cluster(dq4)
est store m1
reghdfe lnhigh_edu station_p $var1 $var2 if down_ind==1, absorb(id dq2#year) cluster(dq4)
est store m2
reghdfe lnlow_edu station_p $var1 $var2 if down_ind==1, absorb(id dq2#year) cluster(dq4)
est store m3
reghdfe lnoccp1 station_p $var1 $var2 if down_ind==1, absorb(id dq2#year) cluster(dq4)
est store m4
reghdfe lnoccp2 station_p $var1 $var2 if down_ind==1, absorb(id dq2#year) cluster(dq4)
est store m5
reghdfe lnoccp3 station_p $var1 $var2 if down_ind==1, absorb(id dq2#year) cluster(dq4)
est store m6
reghdfe lnoccp4 station_p $var1 $var2 if down_ind==1, absorb(id dq2#year) cluster(dq4)
est store m7
reghdfe lnoccp5 station_p $var1 $var2 if down_ind==1, absorb(id dq2#year) cluster(dq4)
est store m8
reghdfe lnoccp67 station_p $var1 $var2 if down_ind==1, absorb(id dq2#year) cluster(dq4)
est store m9
reghdfe lnoccp8 station_p $var1 $var2 if down_ind==1, absorb(id dq2#year) cluster(dq4)
est store m10
reghdfe lnoccp9_11 station_p $var1 $var2 if down_ind==1, absorb(id dq2#year) cluster(dq4)
est store m11


ivreghdfe lnlabor (station_p=iv1 iv2) $var1 $var2 if down_ind==1, absorb(id dq2#year) cluster(dq4)
est store m1
ivreghdfe lnhigh_edu (station_p=iv1 iv2) $var1 $var2 if down_ind==1, absorb(id dq2#year) cluster(dq4)
est store m2
ivreghdfe lnlow_edu (station_p=iv1 iv2) $var1 $var2 if down_ind==1, absorb(id dq2#year) cluster(dq4)
est store m3
ivreghdfe lnoccp1 (station_p=iv1 iv2) $var1 $var2 if down_ind==1, absorb(id dq2#year) cluster(dq4)
est store m4
ivreghdfe lnoccp2 (station_p=iv1 iv2) $var1 $var2 if down_ind==1, absorb(id dq2#year) cluster(dq4)
est store m5
ivreghdfe lnoccp3 (station_p=iv1 iv2) $var1 $var2 if down_ind==1, absorb(id dq2#year) cluster(dq4)
est store m6
ivreghdfe lnoccp4 (station_p=iv1 iv2) $var1 $var2 if down_ind==1, absorb(id dq2#year) cluster(dq4)
est store m7
ivreghdfe lnoccp5 (station_p=iv1 iv2) $var1 $var2 if down_ind==1, absorb(id dq2#year) cluster(dq4)
est store m8
ivreghdfe lnoccp67 (station_p=iv1 iv2) $var1 $var2 if down_ind==1, absorb(id dq2#year) cluster(dq4)
est store m9
ivreghdfe lnoccp8 (station_p=iv1 iv2) $var1 $var2 if down_ind==1, absorb(id dq2#year) cluster(dq4)
est store m10
ivreghdfe lnoccp9_11 (station_p=iv1 iv2) $var1 $var2 if down_ind==1, absorb(id dq2#year) cluster(dq4)
est store m11

reghdfe lnlabor station_p $var1 $var2 if ind_class==3, absorb(id dq2#year) cluster(dq4)
est store m1
reghdfe lnhigh_edu station_p $var1 $var2 if ind_class==3, absorb(id dq2#year) cluster(dq4)
est store m2
reghdfe lnlow_edu station_p $var1 $var2 if ind_class==3, absorb(id dq2#year) cluster(dq4)
est store m3

reghdfe lnoccp1 station_p $var1 $var2 if ind_class==3, absorb(id dq2#year) cluster(dq4)
est store m4
reghdfe lnoccp2 station_p $var1 $var2 if ind_class==3, absorb(id dq2#year) cluster(dq4)
est store m5
reghdfe lnoccp3 station_p $var1 $var2 if ind_class==3, absorb(id dq2#year) cluster(dq4)
est store m6
reghdfe lnoccp4 station_p $var1 $var2 if ind_class==3, absorb(id dq2#year) cluster(dq4)
est store m7
reghdfe lnoccp5 station_p $var1 $var2 if ind_class==3, absorb(id dq2#year) cluster(dq4)
est store m8
reghdfe lnoccp67 station_p $var1 $var2 if ind_class==3, absorb(id dq2#year) cluster(dq4)
est store m9
reghdfe lnoccp8 station_p $var1 $var2 if ind_class==3, absorb(id dq2#year) cluster(dq4)
est store m10
reghdfe lnoccp9_11 station_p $var1 $var2 if ind_class==3, absorb(id dq2#year) cluster(dq4)
est store m11
esttab m1 m2 m3 m4 m5 m6 m7 m8 m9 m10 m11 using "xxxx\附表A7-A.rtf", replace nogaps b(4) se(4) star(* 0.10 ** 0.05 *** 0.01) r2

**技术密集型2SLS（图3a，附表A7 PanelB）
ivreghdfe lnlabor (station_p=iv1 iv2) $var1 $var2 if ind_class==3, absorb(id dq2#year) cluster(dq4)
est store m1
ivreghdfe lnhigh_edu (station_p=iv1 iv2) $var1 $var2 if ind_class==3, absorb(id dq2#year) cluster(dq4)
est store m2
ivreghdfe lnlow_edu (station_p=iv1 iv2) $var1 $var2 if ind_class==3, absorb(id dq2#year) cluster(dq4)
est store m3

ivreghdfe lnoccp1 (station_p=iv1 iv2) $var1 $var2 if ind_class==3, absorb(id dq2#year) cluster(dq4)
est store m4
ivreghdfe lnoccp2 (station_p=iv1 iv2) $var1 $var2 if ind_class==3, absorb(id dq2#year) cluster(dq4)
est store m5
ivreghdfe lnoccp3 (station_p=iv1 iv2) $var1 $var2 if ind_class==3, absorb(id dq2#year) cluster(dq4)
est store m6
ivreghdfe lnoccp4 (station_p=iv1 iv2) $var1 $var2 if ind_class==3, absorb(id dq2#year) cluster(dq4)
est store m7
ivreghdfe lnoccp5 (station_p=iv1 iv2) $var1 $var2 if ind_class==3, absorb(id dq2#year) cluster(dq4)
est store m8
ivreghdfe lnoccp67 (station_p=iv1 iv2) $var1 $var2 if ind_class==3, absorb(id dq2#year) cluster(dq4)
est store m9
ivreghdfe lnoccp8 (station_p=iv1 iv2) $var1 $var2 if ind_class==3, absorb(id dq2#year) cluster(dq4)
est store m10
ivreghdfe lnoccp9_11 (station_p=iv1 iv2) $var1 $var2 if ind_class==3, absorb(id dq2#year) cluster(dq4)
est store m11
esttab m1 m2 m3 m4 m5 m6 m7 m8 m9 m10 m11 using "xxxx\附表A7-B.rtf", replace nogaps b(4) se(4) star(* 0.10 ** 0.05 *** 0.01) r2

**非技术密集型OLS（附表A8 PanelA）
reghdfe lnlabor station_p $var1 $var2 if ind_class<3, absorb(id dq2#year) cluster(dq4)
est store m1
reghdfe lnhigh_edu station_p $var1 $var2 if ind_class<3, absorb(id dq2#year) cluster(dq4)
est store m2
reghdfe lnlow_edu station_p $var1 $var2 if ind_class<3, absorb(id dq2#year) cluster(dq4)
est store m3

reghdfe lnoccp1 station_p $var1 $var2 if ind_class<3, absorb(id dq2#year) cluster(dq4)
est store m4
reghdfe lnoccp2 station_p $var1 $var2 if ind_class<3, absorb(id dq2#year) cluster(dq4)
est store m5
reghdfe lnoccp3 station_p $var1 $var2 if ind_class<3, absorb(id dq2#year) cluster(dq4)
est store m6
reghdfe lnoccp4 station_p $var1 $var2 if ind_class<3, absorb(id dq2#year) cluster(dq4)
est store m7
reghdfe lnoccp5 station_p $var1 $var2 if ind_class<3, absorb(id dq2#year) cluster(dq4)
est store m8
reghdfe lnoccp67 station_p $var1 $var2 if ind_class<3, absorb(id dq2#year) cluster(dq4)
est store m9
reghdfe lnoccp8 station_p $var1 $var2 if ind_class<3, absorb(id dq2#year) cluster(dq4)
est store m10
reghdfe lnoccp9_11 station_p $var1 $var2 if ind_class<3, absorb(id dq2#year) cluster(dq4)
est store m11
esttab m1 m2 m3 m4 m5 m6 m7 m8 m9 m10 m11 using "xxxx\附表A8-A.rtf", replace nogaps b(4) se(4) star(* 0.10 ** 0.05 *** 0.01) r2

**非技术密集型2SLS（图3b，附表A8 PanelB）
ivreghdfe lnlabor (station_p=iv1 iv2) $var1 $var2 if ind_class<3, absorb(id dq2#year) cluster(dq4)
est store m1
ivreghdfe lnhigh_edu (station_p=iv1 iv2) $var1 $var2 if ind_class<3, absorb(id dq2#year) cluster(dq4)
est store m2
ivreghdfe lnlow_edu (station_p=iv1 iv2) $var1 $var2 if ind_class<3, absorb(id dq2#year) cluster(dq4)
est store m3

ivreghdfe lnoccp1 (station_p=iv1 iv2) $var1 $var2 if ind_class<3, absorb(id dq2#year) cluster(dq4)
est store m4
ivreghdfe lnoccp2 (station_p=iv1 iv2) $var1 $var2 if ind_class<3, absorb(id dq2#year) cluster(dq4)
est store m5
ivreghdfe lnoccp3 (station_p=iv1 iv2) $var1 $var2 if ind_class<3, absorb(id dq2#year) cluster(dq4)
est store m6
ivreghdfe lnoccp4 (station_p=iv1 iv2) $var1 $var2 if ind_class<3, absorb(id dq2#year) cluster(dq4)
est store m7
ivreghdfe lnoccp5 (station_p=iv1 iv2) $var1 $var2 if ind_class<3, absorb(id dq2#year) cluster(dq4)
est store m8
ivreghdfe lnoccp67 (station_p=iv1 iv2) $var1 $var2 if ind_class<3, absorb(id dq2#year) cluster(dq4)
est store m9
ivreghdfe lnoccp8 (station_p=iv1 iv2) $var1 $var2 if ind_class<3, absorb(id dq2#year) cluster(dq4)
est store m10
ivreghdfe lnoccp9_11 (station_p=iv1 iv2) $var1 $var2 if ind_class<3, absorb(id dq2#year) cluster(dq4)
est store m11
esttab m1 m2 m3 m4 m5 m6 m7 m8 m9 m10 m11 using "xxxx\附表A8-B.rtf", replace nogaps b(4) se(4) star(* 0.10 ** 0.05 *** 0.01) r2

ivreghdfe lnlabor (station_p=iv1 iv2) $var1 $var2 if industry==1, absorb(id dq2#year) cluster(dq4)
est store m1
ivreghdfe lnhigh_edu (station_p=iv1 iv2) $var1 $var2 if industry==1, absorb(id dq2#year) cluster(dq4)
est store m2
ivreghdfe lnlow_edu (station_p=iv1 iv2) $var1 $var2 if industry==1, absorb(id dq2#year) cluster(dq4)
est store m3

ivreghdfe lnoccp1 (station_p=iv1 iv2) $var1 $var2 if industry==1, absorb(id dq2#year) cluster(dq4)
est store m4
ivreghdfe lnoccp2 (station_p=iv1 iv2) $var1 $var2 if industry==1, absorb(id dq2#year) cluster(dq4)
est store m5
ivreghdfe lnoccp3 (station_p=iv1 iv2) $var1 $var2 if industry==1, absorb(id dq2#year) cluster(dq4)
est store m6
ivreghdfe lnoccp4 (station_p=iv1 iv2) $var1 $var2 if industry==1, absorb(id dq2#year) cluster(dq4)
est store m7
ivreghdfe lnoccp5 (station_p=iv1 iv2) $var1 $var2 if industry==1, absorb(id dq2#year) cluster(dq4)
est store m8
ivreghdfe lnoccp67 (station_p=iv1 iv2) $var1 $var2 if industry==1, absorb(id dq2#year) cluster(dq4)
est store m9
ivreghdfe lnoccp8 (station_p=iv1 iv2) $var1 $var2 if industry==1, absorb(id dq2#year) cluster(dq4)
est store m10
ivreghdfe lnoccp9_11 (station_p=iv1 iv2) $var1 $var2 if industry==1, absorb(id dq2#year) cluster(dq4)
est store m11
esttab m1 m2 m3 m4 m5 m6 m7 m8 m9 m10 m11 using "xxxx\附表A10-B.rtf", replace nogaps b(4) se(4) star(* 0.10 ** 0.05 *** 0.01) r2

**服务业OLS（附表A11 PanelA）
reghdfe lnlabor station_p $var1 $var2 if service==1, absorb(id dq2#year) cluster(dq4)
est store m1
reghdfe lnhigh_edu station_p $var1 $var2 if service==1, absorb(id dq2#year) cluster(dq4)
est store m2
reghdfe lnlow_edu station_p $var1 $var2 if service==1, absorb(id dq2#year) cluster(dq4)
est store m3

reghdfe lnoccp1 station_p $var1 $var2 if service==1, absorb(id dq2#year) cluster(dq4)
est store m4
reghdfe lnoccp2 station_p $var1 $var2 if service==1, absorb(id dq2#year) cluster(dq4)
est store m5
reghdfe lnoccp3 station_p $var1 $var2 if service==1, absorb(id dq2#year) cluster(dq4)
est store m6
reghdfe lnoccp4 station_p $var1 $var2 if service==1, absorb(id dq2#year) cluster(dq4)
est store m7
reghdfe lnoccp5 station_p $var1 $var2 if service==1, absorb(id dq2#year) cluster(dq4)
est store m8
reghdfe lnoccp67 station_p $var1 $var2 if service==1, absorb(id dq2#year) cluster(dq4)
est store m9
reghdfe lnoccp8 station_p $var1 $var2 if service==1, absorb(id dq2#year) cluster(dq4)
est store m10
reghdfe lnoccp9_11 station_p $var1 $var2 if service==1, absorb(id dq2#year) cluster(dq4)
est store m11
esttab m1 m2 m3 m4 m5 m6 m7 m8 m9 m10 m11 using "xxxx\附表A11-A.rtf", replace nogaps b(4) se(4) star(* 0.10 ** 0.05 *** 0.01) r2

**服务业2SLS（图4c，附表A11 PanelB）
ivreghdfe lnlabor (station_p=iv1 iv2) $var1 $var2 if service==1, absorb(id dq2#year) cluster(dq4)
est store m1
ivreghdfe lnhigh_edu (station_p=iv1 iv2) $var1 $var2 if service==1, absorb(id dq2#year) cluster(dq4)
est store m2
ivreghdfe lnlow_edu (station_p=iv1 iv2) $var1 $var2 if service==1, absorb(id dq2#year) cluster(dq4)
est store m3

ivreghdfe lnoccp1 (station_p=iv1 iv2) $var1 $var2 if service==1, absorb(id dq2#year) cluster(dq4)
est store m4
ivreghdfe lnoccp2 (station_p=iv1 iv2) $var1 $var2 if service==1, absorb(id dq2#year) cluster(dq4)
est store m5
ivreghdfe lnoccp3 (station_p=iv1 iv2) $var1 $var2 if service==1, absorb(id dq2#year) cluster(dq4)
est store m6
ivreghdfe lnoccp4 (station_p=iv1 iv2) $var1 $var2 if service==1, absorb(id dq2#year) cluster(dq4)
est store m7
ivreghdfe lnoccp5 (station_p=iv1 iv2) $var1 $var2 if service==1, absorb(id dq2#year) cluster(dq4)
est store m8
ivreghdfe lnoccp67 (station_p=iv1 iv2) $var1 $var2 if service==1, absorb(id dq2#year) cluster(dq4)
est store m9
ivreghdfe lnoccp8 (station_p=iv1 iv2) $var1 $var2 if service==1, absorb(id dq2#year) cluster(dq4)
est store m10
ivreghdfe lnoccp9_11 (station_p=iv1 iv2) $var1 $var2 if service==1, absorb(id dq2#year) cluster(dq4)
est store m11
esttab m1 m2 m3 m4 m5 m6 m7 m8 m9 m10 m11 using "xxxx\附表A11-B.rtf", replace nogaps b(4) se(4) star(* 0.10 ** 0.05 *** 0.01) r2

下面狠多代码都是类似，就不再一一展示，有兴趣的话去官网下载即可，我主要是解决那个代码中可能不能运行的问题





