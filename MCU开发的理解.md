### MCU的概述

ST公司产品STM32采用ARM公司的Cortex-M系列内核，一个微控制器不是CPU，而是CPU加上相关的一些外设的集合，而内核是MCU里面的CPU，内核是ARM公司设计的一个处理器体系结构。ST、TI这些公司不设计CPU内核，而是负责设计CPU外围的一些东西：芯片内部的模数转换外设ADC、串口UART、定时器TIM等等这些外部设备。内核与外设，相当于我们PC上的CPU与主板、内存、显卡、硬盘的关系。

Cortex某个系列芯片的内核是一样的，区别是外设不一样，外设有差异，这些差异会导致软件在同内核，不同外设的芯片上移植困难。这个世界上有不少的MCU公司，都用的是ARM的内核，外设自己搞，为了确保软件的兼容性，ARM与这些公司一起搞了一个CMSIS标准 Cortex MicroController Software Interface Standard.而所谓的CMSIS，就是建立了一个抽象层。


