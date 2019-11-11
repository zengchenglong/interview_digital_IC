## FPGA原理
* [1 FPGA的基本组成](#1-FPGA的基本组成) 
* [2 LUT的工作原理](#2-LUT的工作原理) 

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
