# 一、创建项目模板

```shell
|—— USER                                   #用户代码
|   |—— stm32h7xx_it.c                    #中断服务函数
|
|—— CORE                                  #核心系统文件
|   |—— stm32h7xx_it.c                    #中断服务函数
|   |—— system_stm32h7xx.c                #系统时钟初始化
|
|
|—— HALLIB                                #HAL库支持文件 
|   |—— STM32H7xx_HAL_Driver              #STM32H7xx的核心支持库
|
|—— OUTPUT                                #编译输出文件
|   |—— Listings                          #链接器生成的映射文件
|   |—— Objects                           #编译中间文件
|
|—— KEIL PROJECT                               #IDE工程配置
|   |—— DebugConfig                       #调试器配置文件（如ST-Link/J-Ling配置）
|   |—— *.uvprojx                         #Keil工程文件（项目设置、文件索引）
|

```

![](README_IMGS/Pasted%20image%2020260927013410.png)

# 二、复制支持库文件

## 1、复制HAL库文件到HALLIB下

将<span  style="color: yellow">D:\AlwaysFiles\学习资料\STM32\cube固件资料\stm32cubeh7-v1-13-0\STM32Cube\_FW\_H7\_V1.13.0\Drivers\STM32H7xx\_HAL\_Driver</span> 文件夹直接复制到HALLIB下

![](README_IMGS/Pasted%20image%2020260927013930.png)

## 2、复制core相关文件到CORE下

![](README_IMGS/Pasted%20image%2020260927020526.png)

![](README_IMGS/Pasted%20image%2020260927014246.png)

![](README_IMGS/Pasted%20image%2020260927014421.png)

![](README_IMGS/Pasted%20image%2020260927014328.png)

新建main.c 和 main.h 文件，内容如下：

![](README_IMGS/Pasted%20image%2020260927014912.png)

## 3、新建keil项目到Project文件夹下

![](README_IMGS/Pasted%20image%2020260926212305.png)

## 2、选择开发版型号

![](README_IMGS/Pasted%20image%2020260926212503.png)
![](README_IMGS/Pasted%20image%2020260926212523.png)

Add Group 并添加.c文件
![](README_IMGS/Pasted%20image%2020260927015040.png)

配置编译器为 version5
![](README_IMGS/Pasted%20image%2020260927015150.png)

将KEIL PROJECT 下的 两个文件夹剪切到OUTPUT下
![](README_IMGS/Pasted%20image%2020260927015324.png)

![](README_IMGS/Pasted%20image%2020260927015356.png)

选择存放编译输出结果的文件夹
![](README_IMGS/Pasted%20image%2020260927015216.png)

添加宏定义+h头文件导入路径
![](README_IMGS/Pasted%20image%2020260927015808.png)

选择烧录工具
![](README_IMGS/Pasted%20image%2020260927015844.png)

![](README_IMGS/Pasted%20image%2020260927015938.png)

尝试编译build，报错： 原因是找不到hal\_conf.h文件
![](README_IMGS/Pasted%20image%2020260927020105.png)

发现下载的cube库文件中，给了一个hal\_conf\_template.h模板文件
![](README_IMGS/Pasted%20image%2020260927020314.png)

把它复制粘贴到CORE里，重命名
![](README_IMGS/Pasted%20image%2020260927020404.png)

再次编译报错
![](README_IMGS/Pasted%20image%2020260927020638.png)

主要错误是链接阶段缺少`SystemInit` 和`ExitRun0Mode` 两个符号——这通常是因为工程里没有添加`system_stm32h7xx.c` 文件。将其复制到CORE下

![](README_IMGS/Pasted%20image%2020260927020753.png)

然后再keil里进行add group
![](README_IMGS/Pasted%20image%2020260927021033.png)

最终编译build，成功
![](README_IMGS/Pasted%20image%2020260927021109.png)
