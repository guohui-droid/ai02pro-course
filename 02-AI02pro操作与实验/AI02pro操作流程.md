**AI02pro操作流程**

**设备开机**

箱体供电220v，插好电源线，按下电源按钮"红灯亮起"。

点击开机按钮（工作区面板右下方）

|  |  |
|:--:|:--:|
| ![AI02pro操作流程_assets/media/image1.jpeg](AI02pro操作流程_assets/media/image1.jpeg) | ![AI02pro操作流程_assets/media/image2.jpeg](AI02pro操作流程_assets/media/image2.jpeg) |

**硬件安装模块**

1\. **机械臂安装**

使用四颗滚花手拧螺丝固定机械臂底座，如下图所示

|  |  |
|:--:|:--:|
| ![AI02pro操作流程_assets/media/image3.jpeg](AI02pro操作流程_assets/media/image3.jpeg) | ![AI02pro操作流程_assets/media/image4.jpeg](AI02pro操作流程_assets/media/image4.jpeg) |

注：航插头朝向屏幕

![AI02pro操作流程_assets/media/image5.jpeg](AI02pro操作流程_assets/media/image5.jpeg)

机械臂使用时：需要将航插与对应的航插母头对接。保证机械臂处于上电状态。

**确认舵机正常使用**

打开"C:\ai02pro\project\app\FD1985-250729"目录

![AI02pro操作流程_assets/media/image6.png](AI02pro操作流程_assets/media/image6.png)

双击打开FD.exe

将比特率调到1000000，点击打开

![AI02pro操作流程_assets/media/image7.png](AI02pro操作流程_assets/media/image7.png)

![AI02pro操作流程_assets/media/image8.png](AI02pro操作流程_assets/media/image8.png)

点击搜索，需要看见7个舵机都可以正常使用

![AI02pro操作流程_assets/media/image9.png](AI02pro操作流程_assets/media/image9.png)

依次点击停止，关闭软件

![AI02pro操作流程_assets/media/image10.png](AI02pro操作流程_assets/media/image10.png)

1.1 **修改机械臂Friendly Name**

打开"C:\ai02pro\project\app\usbdeview"目录，鼠标右键单击USBDeview.exe"以管理员身份运行"

![AI02pro操作流程_assets/media/image11.png](AI02pro操作流程_assets/media/image11.png)

需要将"Drive Letter"是"COM8"的Friendly Name修改为"robot"

选中这一行，鼠标右键打开上下文菜单，选择"Open RegEdit"

![AI02pro操作流程_assets/media/image12.png](AI02pro操作流程_assets/media/image12.png)

找到"Friendly Name"这一项进行修改

![AI02pro操作流程_assets/media/image13.png](AI02pro操作流程_assets/media/image13.png)

点击确定即可

![AI02pro操作流程_assets/media/image14.png](AI02pro操作流程_assets/media/image14.png)

依次关闭窗口即可

2\. **相机安装**

相机安装按以下步骤进行

|  |  |
|:--:|:--:|
| ![AI02pro操作流程_assets/media/image15.jpeg](AI02pro操作流程_assets/media/image15.jpeg) | ![AI02pro操作流程_assets/media/image16.jpeg](AI02pro操作流程_assets/media/image16.jpeg) |

|  |  |
|:--:|:--:|
| ![AI02pro操作流程_assets/media/image17.jpeg](AI02pro操作流程_assets/media/image17.jpeg) | ![AI02pro操作流程_assets/media/image18.jpeg](AI02pro操作流程_assets/media/image18.jpeg) |

|  |  |
|:--:|:--:|
| ![AI02pro操作流程_assets/media/image19.jpeg](AI02pro操作流程_assets/media/image19.jpeg) | ![AI02pro操作流程_assets/media/image20.jpeg](AI02pro操作流程_assets/media/image20.jpeg) |

3\. **麦克风使用**

正常模式为灰色即不亮灯，长按旋钮则打开降噪模式即"绿灯状态"，请按一下则静音即"红灯状态"。

旋钮也可以调节收音大小

|  |  |  |
|:--:|:--:|:--:|
| ![AI02pro操作流程_assets/media/image21.jpeg](AI02pro操作流程_assets/media/image21.jpeg) | ![AI02pro操作流程_assets/media/image22.jpeg](AI02pro操作流程_assets/media/image22.jpeg) | ![AI02pro操作流程_assets/media/image23.jpeg](AI02pro操作流程_assets/media/image23.jpeg) |

**知识库启动模块**

双击桌面图标打开应用程序Docker Desktop

![AI02pro操作流程_assets/media/image24.png](AI02pro操作流程_assets/media/image24.png)

(如果Docker Desktop应用已在后台运行，会出现双击图标没反应的情况，点击桌面右下角隐藏图标选项，鼠标左键单击图标打开应用)。

![AI02pro操作流程_assets/media/image25.png](AI02pro操作流程_assets/media/image25.png)

4\. **大模型服务**

默认配置了两个模型beg-m3(embedding模型)和qwen3:8b(大语言模型)需要依次启动

在docker主页面中找到llm_models，点击启动

![AI02pro操作流程_assets/media/image26.png](AI02pro操作流程_assets/media/image26.png)

![AI02pro操作流程_assets/media/image27.png](AI02pro操作流程_assets/media/image27.png)

点击鼠标左键点击LLM_models进入日志，当出现端口号即启动成功

![AI02pro操作流程_assets/media/image28.png](AI02pro操作流程_assets/media/image28.png)

5\. **Ragflow**

在docker主页面中找到ragflow_docker，点击启动，（启动过程较慢，耐心等待）

![AI02pro操作流程_assets/media/image29.png](AI02pro操作流程_assets/media/image29.png)

点击桌面ragflow图标

![AI02pro操作流程_assets/media/image30.png](AI02pro操作流程_assets/media/image30.png)

默认登录admin@chlrob.com账号密码123456qaz。

![AI02pro操作流程_assets/media/image31.png](AI02pro操作流程_assets/media/image31.png)

点击登录，即可进入主页看到创建好的知识库

![AI02pro操作流程_assets/media/image32.png](AI02pro操作流程_assets/media/image32.png)

点击华航唯实-人工智能产品知识库，进行查看。

![AI02pro操作流程_assets/media/image33.png](AI02pro操作流程_assets/media/image33.png)

检索测试

![AI02pro操作流程_assets/media/image34.png](AI02pro操作流程_assets/media/image34.png)

6\. **Dify**

在docker主页面中找到dify_docker，点击启动

![AI02pro操作流程_assets/media/image35.png](AI02pro操作流程_assets/media/image35.png)

点击桌面dify图标

![AI02pro操作流程_assets/media/image36.png](AI02pro操作流程_assets/media/image36.png)

如果进入此页面，点击登录即可。

默认登录admin@chlrob.com账号密码123456qaz。

![AI02pro操作流程_assets/media/image37.png](AI02pro操作流程_assets/media/image37.png)

选择工作流

![AI02pro操作流程_assets/media/image38.png](AI02pro操作流程_assets/media/image38.png)

点击发布

![AI02pro操作流程_assets/media/image39.png](AI02pro操作流程_assets/media/image39.png)

点击运行

![AI02pro操作流程_assets/media/image40.png](AI02pro操作流程_assets/media/image40.png)

运行结果

![AI02pro操作流程_assets/media/image41.png](AI02pro操作流程_assets/media/image41.png)

**数字人启动模块**

1\. **DigitalHuman**

双击桌面图标打开应用程序PQVista

![AI02pro操作流程_assets/media/image42.png](AI02pro操作流程_assets/media/image42.png)

(如果PQVista应用已在后台运行，会显示弹窗PQVista已启动，点击桌面右下角隐藏图标选项，鼠标左键单击图标打开应用)。

![AI02pro操作流程_assets/media/image43.png](AI02pro操作流程_assets/media/image43.png)

![AI02pro操作流程_assets/media/image44.png](AI02pro操作流程_assets/media/image44.png)

语音交互

鼠标右键进入PQVista设置页面，点击聊天

![AI02pro操作流程_assets/media/image45.png](AI02pro操作流程_assets/media/image45.png)

启动

点击智能语音聊天窗口下方启动按钮

![AI02pro操作流程_assets/media/image46.png](AI02pro操作流程_assets/media/image46.png)

使用麦克风进行对话

可以听见一声"智能语音服务已启动"，同时确保智能语音聊天窗口已就绪

![AI02pro操作流程_assets/media/image47.png](AI02pro操作流程_assets/media/image47.png)

完整对话

唤醒词设定为"小华小华"，喊出唤醒词即可得到回复"我在呢~"，可询问知识库问题，如：介绍下AI11

确保xinfernence已配置完成

确保Dify已发布

完整演示见以下视频

**> 附：视频文件「20251203_112748.mp4」，请在 GitBook 中手动上传该文件。**

关闭智能语音聊天窗口，右下角后台不要关， 进入C:\ai02pro\scripts\digital

![AI02pro操作流程_assets/media/image48.png](AI02pro操作流程_assets/media/image48.png)

运行该项目

此时必须保证智能语音聊天一切正常

单击数字人服务.bat脚本

![AI02pro操作流程_assets/media/image49.png](AI02pro操作流程_assets/media/image49.png)

点击桌面gradio图标

![AI02pro操作流程_assets/media/image50.png](AI02pro操作流程_assets/media/image50.png)

进入华航唯实-数字人主页面

![AI02pro操作流程_assets/media/image51.png](AI02pro操作流程_assets/media/image51.png)

使用麦克风与其交互

以下是详细演示视频

**> 附：视频文件「20251203_132137.mp4」，请在 GitBook 中手动上传该文件。**

2\. **LivePortrait**

此项目是制作数字人形象的项目，最好是正脸照五官清晰，产生比较好的效果图如下：

![AI02pro操作流程_assets/media/image52.png](AI02pro操作流程_assets/media/image52.png)

进入C:\ai02pro\user_data\admin\liveportrait

![AI02pro操作流程_assets/media/image53.png](AI02pro操作流程_assets/media/image53.png)

注：必须包含着configs以及里面的配置文件generate.yaml。

准备一张图片以png或jpg为后缀都可以。

此时的目录结构如下：

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr>
<td style="text-align: left;">Plain Text<br />
C:.<br />
│ guang.jpg<br />
├─animations<br />
└─configs<br />
generate.yaml</td>
</tr>
</tbody>
</table>

修改图片名称后，需要更改generate.yaml文件

![AI02pro操作流程_assets/media/image54.png](AI02pro操作流程_assets/media/image54.png)

注：要求源图片路径必须和根目录下的路径保持一致

运行该项目

双击数字人形象生成.bat脚本

![AI02pro操作流程_assets/media/image55.png](AI02pro操作流程_assets/media/image55.png)

![AI02pro操作流程_assets/media/image56.png](AI02pro操作流程_assets/media/image56.png)

稍等一会即可在文件夹中查看到制作好的形象

![AI02pro操作流程_assets/media/image57.png](AI02pro操作流程_assets/media/image57.png)

如下是制作好的形象

![AI02pro操作流程_assets/media/image58.png](AI02pro操作流程_assets/media/image58.png)

**Comfyui启动模块**

![AI02pro操作流程_assets/media/image59.png](AI02pro操作流程_assets/media/image59.png)

保证Docker Desktop已经启动

在"C:\ai02pro\user_data\admin\comfyui"文件目录导航栏中输入powershell

注：文件夹中一定需要包含"docker-compose.yml"文件

![AI02pro操作流程_assets/media/image60.png](AI02pro操作流程_assets/media/image60.png)

输入以下命令

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr>
<td style="text-align: left;">Plain Text<br />
docker compose up</td>
</tr>
</tbody>
</table>

![AI02pro操作流程_assets/media/image61.png](AI02pro操作流程_assets/media/image61.png)

便可在Docker Desktop中看到comfyui已启动。可以将其他启动的容器先关闭，留出空间运行comfyui

![AI02pro操作流程_assets/media/image62.png](AI02pro操作流程_assets/media/image62.png)

点击桌面上comfyui图标

![AI02pro操作流程_assets/media/image63.png](AI02pro操作流程_assets/media/image63.png)

![AI02pro操作流程_assets/media/image64.png](AI02pro操作流程_assets/media/image64.png)

打开左侧导航栏的工作流便可查看已配置好的工作流，点击右上角的运行便可将工作流跑起来

![AI02pro操作流程_assets/media/image65.png](AI02pro操作流程_assets/media/image65.png)

**模仿学习模块**

1\. **机械臂校准**

点击C:\ai02pro\scripts\lerobot下的lerobot_calibrate.bat

![AI02pro操作流程_assets/media/image66.png](AI02pro操作流程_assets/media/image66.png)

![AI02pro操作流程_assets/media/image67.png](AI02pro操作流程_assets/media/image67.png)

注：如果出现以下情况

![AI02pro操作流程_assets/media/image68.png](AI02pro操作流程_assets/media/image68.png)

是已含有校准文件，需要按'c'键后再按'回车键'进行重新校准。

中间位置即每个舵机物理限位的中间角度位置，校准程序将该位置作为每个舵机的零点。如下所示：

![AI02pro操作流程_assets/media/image69.jpeg](AI02pro操作流程_assets/media/image69.jpeg)

调整至中间位置后，按下回车键即完成中间位置校准。

![AI02pro操作流程_assets/media/image70.png](AI02pro操作流程_assets/media/image70.png)

机械臂校准演示

**> 附：视频文件「IMG_2556.MOV」，请在 GitBook 中手动上传该文件。**

完成校准后，按下回车键结束

![AI02pro操作流程_assets/media/image71.png](AI02pro操作流程_assets/media/image71.png)

2\. **机械臂遥操**

注：保证机械臂校准完成

点击C:\ai02pro\scripts\lerobot下的lerobot_teleoperate.bat

![AI02pro操作流程_assets/media/image72.png](AI02pro操作流程_assets/media/image72.png)

![AI02pro操作流程_assets/media/image73.png](AI02pro操作流程_assets/media/image73.png)

可以看到摇操画面

![AI02pro操作流程_assets/media/image74.png](AI02pro操作流程_assets/media/image74.png)

键盘遥操的按键设置

|          |                         |
|:---------|:------------------------|
| **按键** | **功能**                |
| w        | 沿 X 轴正向移动         |
| s        | 沿 X 轴负向移动         |
| a        | 沿 Y 轴正向移动         |
| d        | 沿 Y 轴负向移动         |
| e        | 沿 Z 轴正向移动         |
| q        | 沿 Z 轴负向移动         |
| y        | 翻滚角 (Roll) 正向旋转  |
| u        | 翻滚角 (Roll) 负向旋转  |
| h        | 俯仰角 (Pitch) 正向旋转 |
| j        | 俯仰角 (Pitch) 负向旋转 |
| m        | 偏航角 (Yaw) 正向旋转   |
| n        | 偏航角 (Yaw) 负向旋转   |
| r        | 打开夹爪                |
| f        | 关闭夹爪                |

3\. **数据集录制**

注：保证机械臂校准完成

点击C:\ai02pro\scripts\lerobot下的lerobot_record.bat

![AI02pro操作流程_assets/media/image75.png](AI02pro操作流程_assets/media/image75.png)

![AI02pro操作流程_assets/media/image76.png](AI02pro操作流程_assets/media/image76.png)

根据语音提示进行采集数据

4\. **模型训练**

点击C:\ai02pro\scripts\lerobot下的lerobot_train.bat

![AI02pro操作流程_assets/media/image77.png](AI02pro操作流程_assets/media/image77.png)

![AI02pro操作流程_assets/media/image78.png](AI02pro操作流程_assets/media/image78.png)

**视觉引导抓取模块**

注：1. 保证相机安装完成

保证机械臂安装完成

保证机械臂已完成校准

1\. **相机标定**

点击C:\ai02pro\scripts\grasp下的相机标定.bat脚本

![AI02pro操作流程_assets/media/image79.png](AI02pro操作流程_assets/media/image79.png)

![AI02pro操作流程_assets/media/image80.png](AI02pro操作流程_assets/media/image80.png)

注：保证标定板无遮挡

![AI02pro操作流程_assets/media/image81.png](AI02pro操作流程_assets/media/image81.png)

点击相机实时窗口，按下"s"保存

![AI02pro操作流程_assets/media/image82.png](AI02pro操作流程_assets/media/image82.png)

2\. **视觉引导抓取**

点击C:\ai02pro\scripts\grasp下的抓取执行.bat脚本

![AI02pro操作流程_assets/media/image83.png](AI02pro操作流程_assets/media/image83.png)

![AI02pro操作流程_assets/media/image84.png](AI02pro操作流程_assets/media/image84.png)

将绿色物料，放到作业区域，按下"空格键"

![AI02pro操作流程_assets/media/image85.jpeg](AI02pro操作流程_assets/media/image85.jpeg)

以下是演示视频

**> 附：视频文件「IMG_1977.MOV」，请在 GitBook 中手动上传该文件。**

完成后，在终端按下"control+C"退出

![AI02pro操作流程_assets/media/image86.png](AI02pro操作流程_assets/media/image86.png)

**机械臂摇操模块**

打开："C:\ai02pro\user_data\admin\teleop_robot\configs"可以查看三个yaml文件

![AI02pro操作流程_assets/media/image87.png](AI02pro操作流程_assets/media/image87.png)

以下是参数是"keyboard_sam01.yaml"

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr>
<td style="text-align: left;">YAML<br />
# 控制器参数<br />
controller:<br />
type: keyboard # 控制器类型：gamepad(手柄)，keyboard(键盘)，handpose(手势)<br />
step_sizes: # 步幅<br />
x: 0.001<br />
y: 0.001<br />
z: 0.001<br />
roll: 0.01 # 旋转角步幅<br />
pitch: 0.01 # 俯仰角步幅<br />
yaw: 0.01 # 偏航角步幅<br />
gripper: 0.01 # 夹爪步幅<br />
viewer:<br />
scene_path: C:/ai02pro/project/teleop_robot/models/sam01_robot_left/urdf/scene.xml<br />
distance: 1.5 # 摄像机高度<br />
azimuth: 150 # 摄像机方位角<br />
elevation: -20 # 摄像机仰角<br />
# 运动学参数<br />
kinematics:<br />
urdf_path: C:/ai02pro/project/teleop_robot/models/sam01_robot_left/urdf/sam01_robot.xml<br />
target_frame_name: joint6<br />
position_weight: 20.0<br />
rotation_weight: 1<br />
last_joint_as_gripper: false<br />
last_joint_name: joint7<br />
# 机械臂参数<br />
# robot:<br />
# type: sam01 # 机械臂类型<br />
# port: robot # COM口<br />
# calibration_path: C:/ai02pro/user_data/test/lerobot/calibration/robot_arm_follower.json # 校准文件路径<br />
# reverse_gripper: true # 夹爪关节逆变换<br />
# 全局参数<br />
init_joints: [0, 1.55, -1.55, 0, 0, 0, 0.0] # 初始关节角<br />
position_low_bound: [-0.8, -0.8, 0] # 末端位置下限<br />
position_up_bound: [0.8, 0.8, 0.8] # 末端位置上限<br />
roll_joint_index: 5 # roll角对应关节索引<br />
pitch_joint_index: 3 # pitch角对应关节索引<br />
yaw_joint_index: 4 # yaw角对应关节索引<br />
gripper_limit: [0, 1.6] # 夹爪关节范围</td>
</tr>
</tbody>
</table>

注意：建议将上述参数的robot相关参数先注释掉，即先不控制机械臂实体，在仿真中调试到最佳状态后再将注释打开，控制机械臂。

1\. **键盘摇操**

点击"C:\ai02pro\scripts\teleop"中的键盘遥操.bat脚本

![AI02pro操作流程_assets/media/image88.png](AI02pro操作流程_assets/media/image88.png)

![AI02pro操作流程_assets/media/image89.png](AI02pro操作流程_assets/media/image89.png)

|             |                        |
|:------------|:-----------------------|
| **按键**    | **功能**               |
| 上方向键(↑) | 沿 X 轴向前移动        |
| 下方向键(↓) | 沿 X 轴向后移动        |
| 左方向键(←) | 沿 Y 轴向左移动        |
| 右方向键(→) | 沿 Y 轴向右移动        |
| x           | 沿 Z 轴升高 (向上移动) |
| z           | 沿 Z 轴降低 (向下移动) |
| r           | 打开夹爪               |
| t           | 关闭夹爪               |
| q           | 末端向左旋转           |
| e           | 末端向右旋转           |
| w           | 抬头                   |
| s           | 低头                   |
| a           | 左偏                   |
| d           | 右偏                   |

以下是演示视频

**> 附：视频文件「IMG_1978.MOV」，请在 GitBook 中手动上传该文件。**

结束后"control+C"退出程序，同时关闭终端窗口

![AI02pro操作流程_assets/media/image90.png](AI02pro操作流程_assets/media/image90.png)

2\. **手柄摇操**

点击"C:\ai02pro\scripts\teleop"中的手柄遥操.bat脚本

![AI02pro操作流程_assets/media/image91.png](AI02pro操作流程_assets/media/image91.png)

使用罗技标准手柄，**使用前请确认手柄控制模式为D（Direct），MODE指示灯为熄灭状态**

|  |  |
|:--:|:--:|
| ![AI02pro操作流程_assets/media/image92.png](AI02pro操作流程_assets/media/image92.png) | ![AI02pro操作流程_assets/media/image93.png](AI02pro操作流程_assets/media/image93.png) |

按键：

|               |                         |
|:--------------|:------------------------|
| **按键**      | **功能**                |
| 左摇杆(上下)  | 控制沿 X 轴的前后移动   |
| 左摇杆 (左右) | 控制沿 Y 轴的左右移动   |
| 右摇杆(上下)  | 控制沿 Z 轴的升高和降低 |
| 上方向键      | 抬头                    |
| 下方向键      | 低头                    |
| 左方向键      | 左偏                    |
| 右方向键      | 右偏                    |
| LB            | 末端向左旋转            |
| RB            | 末端向右旋转            |
| LT            | 打开夹爪                |
| RT            | 关闭夹爪                |

![AI02pro操作流程_assets/media/image94.png](AI02pro操作流程_assets/media/image94.png)

3\. **手势摇操**

手势控制需搭配3D相机使用。相机的角度可以有几种配置：垂直向下、水平向前、水平向右。

![AI02pro操作流程_assets/media/image95.png](AI02pro操作流程_assets/media/image95.png)

启动命令：

点击"C:\ai02pro\scripts\teleop"中的手势遥操.bat脚本

![AI02pro操作流程_assets/media/image96.png](AI02pro操作流程_assets/media/image96.png)

注意：建议将上述参数的robot相关参数先注释掉，即先不控制机械臂实体，在仿真中调试到最佳状态后再将注释打开，控制机械臂。

目前手势控制只能控制xyz位置，无法控制旋转角度。因此初始化时需要将机械臂先调整到合适状态，如上图所示。

程序启动后，需要先初始化手部位置，使得手处于摄像头画面中间位置，如下图所示：

![AI02pro操作流程_assets/media/image97.png](AI02pro操作流程_assets/media/image97.png)

如果需要结束控制，则将手掌变为握拳状态，程序识别到该姿态后即可退出。

整体控制效果演示：

**> 附：视频文件「微信视频2025-12-04_114800_488.mp4」，请在 GitBook 中手动上传该文件。**

**单片机模块**

将"C:\ai02pro\project\speech"拖到vscode图标上，使用vscode打开

![AI02pro操作流程_assets/media/image98.png](AI02pro操作流程_assets/media/image98.png)

激活环境

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr>
<td style="text-align: left;">YAML<br />
conda activate digital</td>
</tr>
</tbody>
</table>

![AI02pro操作流程_assets/media/image99.png](AI02pro操作流程_assets/media/image99.png)

查看交互页面

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr>
<td style="text-align: left;">YAML<br />
python sensor_display.py</td>
</tr>
</tbody>
</table>

![AI02pro操作流程_assets/media/image100.png](AI02pro操作流程_assets/media/image100.png)

![AI02pro操作流程_assets/media/image101.png](AI02pro操作流程_assets/media/image101.png)

控制单片机

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr>
<td style="text-align: left;">YAML<br />
cd sensor</td>
</tr>
</tbody>
</table>

![AI02pro操作流程_assets/media/image102.png](AI02pro操作流程_assets/media/image102.png)

![AI02pro操作流程_assets/media/image103.png](AI02pro操作流程_assets/media/image103.png)

使用方法均一致，python + test_xxx.py

![AI02pro操作流程_assets/media/image104.png](AI02pro操作流程_assets/media/image104.png)
