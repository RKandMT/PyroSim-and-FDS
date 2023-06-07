# 0. 基础操作
1. 鼠标左键：框选
2. 鼠标右键：旋转
3. 鼠标中键：平移
4. Ctrl+R：切换到z轴向下俯视模型

# 1. 建模
## 1. 新建PyroSim程序文件并保存和命名
1. 建模开始之前，确保使用的是SI单位。
## 2. 定义反应和材料数据
1. 材料数据库
    1. Model-Edit Libraries-Category选项卡
    2. Extra Species：额外的物质
    3. Gas-phase Reactions：气相的反应
    4. Heat Detector Models：热探测器模型
    5. Materials：材料
    6. Particles：微粒
    7. Smoke Detector Models：烟雾报警器模型
    8. Spray Models：喷雾模型
    9. Sprinkler Link Models：喷头连接模型
    10. Surface：表面
2. 反应
    
    1. 反应用于定义燃烧的火源参数，通过定义燃烧反应、设置火灾产物、热释放速率等参数使得模拟更接近实际火灾的燃烧过程
    2. 导入反应库：Model-Edit Libraries-Category-Gas phase Reactions
    3. 新建反应：Model-Edit Reaction...-New...
3. 材料
    1. 创建新材料：Model-Edit Materials
    2. 导入材料：Model-Edit Libraries...-Category-Materials
    3. 材料编辑：Model-Edit Materials-New...
          
        Material Type：材料类型（固体材料、液体燃料）
        
        Specific Heat：比热容，可以定义为温度的函数
        
        Conductivity：导热率，可以定义为温度的函数
        
        Emissivity：辐射率，最高为1.0
        
        Absorption Coefficient：吸收系数，反映了吸收热辐射的深度
        
## 3. 创建网格
1. 树状菜单-双击Meshes-New。

    建议使用系统推荐的网格划分数量。
## 4. 定义和创建物体表面属性
1. 定义燃烧器表面

    树状菜单-双击Surfaces-New-名称：Fire；类别：Burner

    在Heat Releases Rate Per Area (HRRPUA) 中输入 500.0 kW/m2
2. 表面（Surfaces）
    
    1. 表面是用来定义固体对象或通风口的属性的。可以在混合物（Mixtures）、层集合（Layers）类的表面中应用先前定义的材料。默认情况下，所有的固体对象和通风口都是惰性绝缘的，温度不变并与外界温度一致。表面除了可以定义固体的导热率，还可以用于定义火源、给通风口一个进风速度等。
    2. 创建表面：Model-Edit Surface-New...
    3. 内置表面：

        1. 绝热表面（ADIABATIC）：表面温度不变，没有热传递
        2. 惰性表面(INERT)：温度变化不明显，热量可以从环境气体到惰性表面发生传递
        3. 镜子表面(MIRROR)：只用于外部网格边界的通风，目的是使整个网格边界适用于两倍大小的对称区域，在模拟中这种表面应该不激活
        4. 开放表面(OPEN)：只用于外部网格边界的通风口，在模拟中应该不激活
     4. 表面类型
        
        除了默认内置表面，用户还可以创建一些常用的表面类型
        1. 绝热（Adiabatic）
        2. 惰性（Inert）
        3. 燃烧（Burner）
            
            HRRPUA：单位面积热释放速率
            
            Mass Lose Rate：单位面积单位时间质量损失率率            
            
            Ramp-Up Time：在仿真开始时，这种表面不会燃烧。此字段允许用户描述释放热量是如何从环境之上升到设定值
            
            Extinguishing Coefficient：灭火系数，用于控制水来灭火
            
            Emissivity：控制热辐射量
         4. 加热或冷却表面（Heater/Cooler）：代表一种热辐射源
         5. 供气表面（Supply）
         6. 排气表面（Exhaust）
         7. 风扇表面（Fan）
         8. 分层表面（Layered）
              
            分层表面是由一层或多层物质组成的，材料包括固体或液体物质。这种类型的表面对于现实世界由材料组成的墙壁和其他物体来说是理想的
            
            1. 材料层（Material Layers）
                
                Layers Divide：用户自定义分层数，其描述值必须小于等于1
                
                Thickness：材料层厚度
                
                Material Composition：一层（行）中，基于质量分数用户可以指定多种材质
                
                Edit：指定使用备用表中已经存在的材料
            2. 表面属性（Surfaces Props）

                Enable Leakage：允许用户在整个表面上选择两个压力区用于泄漏
                
                Initial Internal Temperature：固体内初始温度
                
                Backing：定义固体后表面（内部）的边界条件。默认值Air Gap代表了现实环境中空气间隙，Exposed（暴露）允许边界将热量转移到墙后的空间去，Insulated（隔热）组织了边界上的任何热的损失
                
                Gap Temperature：固体后表面的空气间隙温度，该选项仅在Air Gap选中时可用
                
                Temperature Ramp：制定了表面温度从环境温度到指定的表面问的的增长方式
            3. 反应（Reaction）
            4. 热（Thermal）
            5. 几何尺寸（Geometry）
            6. 物质注入（Species Injection）
            7. 粒子注入（Particle Injection）
         9. 漏气表面（Air Leak）
## 5. 创建实体构筑物
1. 创建燃烧器

  1. 使用通风口Vent创建火源
  
      1. 快捷功能菜单-New Vent或快捷绘图菜单-Draw a Vent
  
      2. 定义ID
  
      3. Surfaces-刚刚建立的Fire表面
  
      4. Geometry标签-定义/修改几何位置和尺寸
      
2. 几何模型可以分组建立：Model-右键New Group...
3. 创建障碍物（OBST）：
    1. Model-New Obstruction  
    2. 通用属性选项卡：
    
        Description：对对象属性的描述，此值不会影响模拟的结果
        
        Group：选择所在的模型组
        
        Activation：绑定此对象来激活新的或现有的控制逻辑，用来添加或删除基于时间或测量条件的对象
        
        Specify Color：颜色
        
        Relative to Object：当纹理被附加到一个对象时，它们基于一个起点平铺开来。在默认情况下，这个点就是原点，相对于对象的最小点默认为定位点
        
        X,Y,Z：这些偏置值基于默认的纹理原点。如果原点与对象有关，则其停留在零，使用对象的最小点
        
        Smooth：放置在弯道处产生涡流
        
        Thicken：当此选项被选中时，这个对象不会成为2D面
        
        Record BNDF：当此选项被选中时，这个对象包括在边界的数据输出中
        
        Permit Holes：当此选项被选中时，同过创建孔可以改变这个对象的几何形状
        
        Allow Holes：使该对象有可能成为通风口的支撑对象
        
        Removable：使物体有可能从激活事件或者BURN_AWAY表面选项的模拟中删除
        
        Display as Outline：改变在Smokeview中此选项的外观
        
        Bulk Density：使用此选项可以覆盖物体所提供的燃料数量
4. 创建洞口（Hole）：略
5. 创建通风口（Vent）：
    1. Model-New Vent
    2. 通风设置不同的表面Surfaces来实现扩散、回风、火焰等效果
    3. 通用选项：
    
        Surface：表面属性决定了通风口的主要功能
        
        Spread Rate：用户可以自定义火焰的蔓延速率
        
        X,Y,Z：火焰从该坐标开始蔓延，只有设置完蔓延速率才能输入坐标
6. 创建板块（Slab）：主要用于屋顶（略）
7. 创建粒子云（Particle Cloud）：用于模拟火灾环境中一些化学物质的变化（略）  
## 6. 创建网格通风口
1. New Vent
2. Surfaces-OPEN
## 7. 创建各种探测设备和消防灭火设备
1. 添加热电偶
    1. 主菜单-Devices-New Thermocouple
    2. 定义NAME
    3. 填写坐标Location
2. 固相监测设备：
    
    1. Devices-New Solid Device...
    2. 输入名称NAME
    3. 选择监测的数据量Quantity
    
        Mass Flux：各种额外的物质的质量流量
        
        Accumulated Mass Per Unit Area：单位面积的累计质量
        
        Cooling Per Unit Area：单位面积降温
        
        Mass Per Unit Area：单位面积质量
        
        Adibatic Surface Temperature：绝热表面温度
        
        Back Wall Temperature：后壁温度
        
        Burning Rate：燃烧率
        
        Convective Heat Flux：对流热流量
        
        Gas Temperature：气体温度
        
        Heat Flux：热流量
        
        Heat Transfer Coefficient：传热系数
        
        Incident Heat Flux：入射热流量
        
        Mass Loss：质量损失
        
        Normal Velocity：法向速度
        
        Radiative Heat Flux：热射热通量
        
        Radiometer：辐射表
        
        Surface Density：表面密度
        
        Wall Temperature：墙的温度
        
        Wall Thickness：墙的厚度
    4. 输入设备的坐标位置Location，对于固相设备，将其放置在一个表面上
    5. Normal of  Solid：表示物体表面的参数，如监测设备位于被侧面的x正向，则x=1；反之x=-1
    6. Rotation可以为0
## 8. 创建各种结果记录
1. 添加温度切片平面
    1. 菜单-Output-2D Slices或快捷绘图菜单-Draw a Planer Slice
    2. 填写单元格：
    
        XYZ Plane:Y;Plane Value:0.0;Gas Phase Quantity:Temperature;Use Vector:NO
    3. 层分区设备：
    
        Devices-New Layer Zoning Device...
2. 实体轮廓 
    1. Output-Edit Solid Profiles
    2. ID：实体轮廓名称
    3. X,Y,Z：在面上将被实体轮廓检验的一个点的坐标（注意：测量的表面必须是导热的）
    4. ORIENT：将被实体轮廓检验的面的方向。如果生成对象顶部的实体轮廓输出结果，此值为+Z
    5. QUANTITY：要被测量的数量（温度、密度）
    6. 输出的结果被保存在ID_prof_n.csv中
3. 边界数量
    1. Output-Boundary Quantities
    2. 壁温：WALL_TEMPERATURE
4. 等值面
    1. Output-Isosurfaces
    2. 在轮廓值（Contour Value）列中输入用于显示的值，多个值用英文分号隔开
5. 绘制3D数据
    1. Plot 3D Data储存的是某一个时刻的静态数据
    1. Output-Plot 3D Data
    2. 选择想要输出的数据，最多支持五个   
6. 数据统计
    1.  Output-Statistics
    2.  用户可以插入一个统计收集设备，它会输出一定网格中的一个特定量的最大值、最小值、平均值等数据
    3.  可以通过二维图表来查看：快捷功能菜单-Plot Device Results
    4.  输出文件将被命名为ID_devc.csv        
## 9. 模型检查

## 10. 储存模型

# 2. 运行求解
## 1. 设置模型属性
1. 设置火灾模拟时间

    菜单栏-Analysis-Simulation Parameters-Time
## 2. 开始模拟

# 3. 分析处理
## 1. 查看分析结果
1. 查看热释放（即火焰）：3D Smoke-HRRPUV
2. 显示3D烟雾：3D Smoke-SOOT DENSITY
3. 查看温度切面：2D Slices-TEMPERATURE
4. 绘制时间历史结果图：快捷功能菜单-Plot Time History Results-保存为csv文件
5. 绘制热偶点时间历史结果图：快捷功能菜单-Plot Device Results
## 2. 分析处理评估结果




# 2. 导入CAD模型
菜单栏-File-Import FDS/CAD Files...

# 4. 设定剖面
树状菜单-Views-Add Scetion Box
