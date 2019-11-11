## FPGA原理
* [1 FPGA的基本组成](#1-FPGA的基本组成) 
* [2 LUT的工作原理](#2-LUT的工作原理) 
* [3 FPGA设计流程](#3-FPGA设计流程) 
* [4 ASIC设计基本流程及工具](#4-ASIC设计基本流程及工具) 
* [5 ASIC设计与FPGA设计的区别](#5-ASIC设计与FPGA设计的区别) 

### 1 FPGA的基本组成
如图1-1所示，FPGA芯片主要由可编程输入输出单元(IOB)、可编程逻辑单元、时钟管理单元、丰富的布线资源以及嵌入式专用模块(DSP、BRAM等)组成。
对于可编程逻辑单元，Xilinx和Intel两大FPGA厂商对其命名有所不同，分别为CLB(Configurable Logic Block)和LAB(Logic Array Block)。这里
以CLB为例，具体介绍可编程逻辑单元。每个CLB包含多个Slice，而每个Slice则由LUT、MUX、进位链和寄存器组成。通常情况下，寄存器的数目是LUT数
目的两倍。在Virtex-2 FPGA中，每个Slice包含2个LUT；在Virtex-6 FPGA中，每个Slice则包含4个LUT。  
<p align="center">  
    <img src=https://github.com/zcl-tju/interview_digital_IC/blob/master/img/1-1.png width="60%" height="60%"/> 
    <p align="center">  
        图1-1 FPGA基本结构

### 2 LUT的工作原理
LUT主要用于实现组合逻辑功能，其本质是一个RAM。目前FPGA中，多使用4输入的LUT，每个LUT可以看成一个有4位地址线的RAM。当用户用硬件描述语言
描述一个逻辑电路后，FPGA开发软件将自动计算逻辑电路中所有可能的结果，并将结果事先写入RAM。这样，每输入一个信号进行逻辑运算就等于输入一个
地址进行查表，找到地址对应的内容，然后输出。表1-1给出一个使用LUT实现4输入与门电路的真值表。  
<p align="center">  
    表1-1 4输入与门增值表
<p align="center">  
    <img src=https://github.com/zcl-tju/interview_digital_IC/blob/master/img/list1-1.jpg width="60%" height="60%"/>  

### 3 FPGA设计流程
* 功能定义/器件选型 (详述)
* 设计输入 (RTL设计)
* 功能仿真 (验证代码功能的正确性)
* 综合 (将RTL映射为门级逻辑网表)
* 综合后仿真 (仿真模型中添加标准延时文件)
* 实现与布局布线 (将逻辑网表映射到FPGA开发板上，并连线)
* 时序仿真 (将延时信息反标注到逻辑网表中)
* FPGA芯片编程与调试 (常用的Debug工具有：vivado debug core, quartus signaltab)  

### 4 ASIC设计基本流程及工具
* 需求分析，架构设计，功能描述
* RTL设计
* 功能仿真 (VCS)
* 逻辑综合 (DC)
* 静态时序分析 (PT)
* 门级仿真 (VCS)
* DFT
* 布局布线 (Astro)
* 静态时序分析 (PT)
* 后仿真 (VCS)

### 5 ASIC设计与FPGA设计的区别
FPGA和ASIC区别很多。**ASIC的逻辑资源通常远远大于FPGA**，逻辑门数目上有数量级的差别，**运行时钟也远远高于FPGA**。而且，ASIC只有一次机会，FPGA可以编程，coding的灵活性相对提高。仅仅从RTL设计上来说:  
(1) ASIC更趋于保守，对逻辑的任何改动都要三思，并且要做备选的选择，以防改错。RTL的任何修改几乎都是增量修改，即便以前的逻辑错了，也不会删掉，而是多做一个分支。  
(2) **ASIC对coding style的要求更高**。所有模块的coding风格要求一致，这样有利于后端以及后续的check。  
(3) **ASIC设计对时钟和复位更加重视**。尤其是时钟，对ASIC的设计极其关键，复位对BIST测试又很关键。ASIC在这方面都需要采用库来进行设计。ASIC通常不会用counter分频，这样会导致时钟不干净，除非是很低频的时钟。ASIC对于跨时钟域的信号处理也谨慎很多。对于clock的关闭和打开也需要严格检查。  
(4) **ASIC要考虑SCAN测试和BIST的问题**，所以设计的时候还需要为SRAM做BIST插入，需要为SCAN预留接口，虽然大部分都是工具干的，但是经常RTL作者也要手动做一些顶层工作，比如SCAN时钟的来源等逻辑。  
(5) **FPGA多用现成IP，需要考虑资源的均衡，不能把某一资源撑爆了，而且FPGA存在资源浪费问题。ASIC很少考虑这种问题，ASIC考虑的永远是性能和功耗**，在逻辑选择上除了SRAM，CLK和复位相关，都是手写的，逻辑基本没有浪费，也更加紧凑。  
(6) ASIC时序预见性更好，可调整度高，所以可以写很大的逻辑。  
*注：觉得太多就看加粗部分吧*
