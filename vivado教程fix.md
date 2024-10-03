1. 自己装一个VIVADO，我用的是2019.2版本，大家随意，但是最好版本不要比我的老。比较大27G左右。不要在苹果虚拟机上跑。组件可以参照下面这个图做选择，否则装完更大：![img](C:\Users\Lenovo\Desktop\vivadooo\be4a753def0afdeb368c42ddc046ea81.jpg)

2. 在本课程“资料”文件夹下载一个HECTemp的压缩包，解压缩后放到本地一个文件夹中，注意，一般国外的软件路径中不要有中文。这是一个工程模板，因为远程实验平台的配置我不大知道，所以直接下载了一个模板，简化了一下。![image-20241003183144197](C:\Users\Lenovo\Desktop\vivadooo\image-20241003183144197.png)

3. 打开VIVADO，注意，不是VIVADO HLS。

4. 在file-->project-->open中，打开HECTemp这个模板工程。可以看到这是一个空的模板工程。![image-20241003183344180](C:\Users\Lenovo\Desktop\vivadooo\image-20241003183344180.png)

5. file->projects->save as另存一下，起一个跟你实验相关的名字。以后用这个模板都另存成跟某个实验相关的名字。比如说咱们是四选一选择器实验。（目的是可读性好，另外保留一个干净的模板文件）![image-20241003183615981](C:\Users\Lenovo\Desktop\vivadooo\image-20241003183615981.png)

6. file->add sources(Alt+A)添加一个.V文件。![image-20241003183736667](C:\Users\Lenovo\Desktop\vivadooo\image-20241003183736667.png)

   ![image-20241003183808708](C:\Users\Lenovo\Desktop\vivadooo\image-20241003183808708.png)

   ![image-20241003183841196](C:\Users\Lenovo\Desktop\vivadooo\image-20241003183841196.png)

   ![image-20241003183915920](C:\Users\Lenovo\Desktop\vivadooo\image-20241003183915920.png)

   ![image-20241003184000611](C:\Users\Lenovo\Desktop\vivadooo\image-20241003184000611.png)

7.  把下面这段代码拷贝进去

   ![image-20241003184058422](C:\Users\Lenovo\Desktop\vivadooo\image-20241003184058422.png)

   ![image-20241003192915189](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20241003192915189.png)

   ```vivado
   `timescale 1ns / 1ps
   
   module mutx4_2(
   
       input sw6_a1,
   
       input sw5_a0,
   
       input sw4_d4,
   
       input sw3_d3,
   
       input sw2_d2,
   
       input sw1_d1,
   
       output led8_out
   
       );
   
       assign led8_out = sw6_a1&sw5_a0&sw4_d4 | (!sw6_a1)&sw5_a0&sw3_d3 | sw6_a1&(!sw5_a0)&sw2_d2 | (!sw6_a1) & (!sw5_a0)&sw1_d1;
   
   endmodule
   ```

8.  Alt+A或者file->第二个选项, 建个约束文件![image-20241003184413838](C:\Users\Lenovo\Desktop\vivadooo\image-20241003184413838.png)

   然后全点ok

   ![image-20241003184508595](C:\Users\Lenovo\Desktop\vivadooo\image-20241003184508595.png)

   ```vivado
   #LEDS
   
   set_property -dict {PACKAGE_PIN B24 IOSTANDARD LVCMOS33} [get_ports {led8_out}]
   
   
   
   #DIP_SW
   
   set_property -dict {PACKAGE_PIN T3 IOSTANDARD LVCMOS33} [get_ports {sw1_d1}]
   
   set_property -dict {PACKAGE_PIN J3 IOSTANDARD LVCMOS33} [get_ports {sw2_d2}]
   
   set_property -dict {PACKAGE_PIN M2 IOSTANDARD LVCMOS33} [get_ports {sw3_d3}]
   
   set_property -dict {PACKAGE_PIN P1 IOSTANDARD LVCMOS33} [get_ports {sw4_d4}]
   
   set_property -dict {PACKAGE_PIN P4 IOSTANDARD LVCMOS33} [get_ports {sw5_a0}]
   
   set_property -dict {PACKAGE_PIN L5 IOSTANDARD LVCMOS33} [get_ports {sw6_a1}]
   ```

9. 下面就可以综合（SYNTHESIS）、实现(IMPLIMENTATION)和生成bit流文件了。使用一个generate bitstream就可以一次性完成这三个步骤。这个时间较长，具体多长时间取决于你机器的CPU。如果苹果虚拟机上跑，可能得20多分钟。![image-20241003184730556](C:\Users\Lenovo\Desktop\vivadooo\image-20241003184730556.png)

   代码飘红就是报错了, 多看看有没有复制错的地方

   中间还有一些步骤, 全点蓝色的ok按钮

   运行完长这样

   ![image-20241003191213636](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20241003191213636.png)

   10. 找到**项目名称.bit**文件

       ![image-20241003193129146](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20241003193129146.png)

       ![image-20241003193242290](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20241003193242290.png)

       ![image-20241003193305156](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20241003193305156.png)![image-20241003193321066](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20241003193321066.png)![image-20241003193442041](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20241003193442041.png)

       

   

   ![image-20241003191644580](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20241003191644580.png)

   后面的网址不好使了...