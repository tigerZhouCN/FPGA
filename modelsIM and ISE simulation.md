使用第三方模拟器（如modelsim）需要在系统搜索路径中定义ModelSim的可执行文件，并且系统上可以使用执行HDL仿真所需的许可证。
Vivado_hls与modelsim联合仿真的路径设置方法：
将modelsim的安装路径加在vivado_hls安装路径前面。
参考：https://www.xilinx.com/support/answers/43271.html
具体方法：
开始-所有程序-Xilinx design tools-vivado 2016.4-vivado hls-vivado hls 2016.4右键属性，改变路径：
D:\xilinx\Vivado_HLS\2016.4\bin\vivado_hls.bat改为：
D:\modeltech64_10.4\win64\modelsim.exe D:\xilinx\Vivado_HLS\2016.4\bin\vivado_hls.bat
前面是modelsim的安装路径，后面是vivado_hls的安装路径。
![image](https://github.com/tigerZhouCN/picture/blob/master/picture/vivado%E5%92%8Cmodelsim%E8%81%94%E5%90%88%E4%BB%BF%E7%9C%9F.png) 
