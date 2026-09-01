**AI02pro模仿学习实验指导书**

1\. **环境安装**

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr>
<td style="text-align: left;">Shell<br />
# python3.12环境<br />
conda install pinocchio<br />
pip install torch==2.7.1 torchvision==0.22.1 --index-url https://download.pytorch.org/whl/cu128<br />
pip install -e ".[feetech,gamepad,kinematics]"<br />
cd libs<br />
pip install pyorbbecsdk-2.0.15-cp312-cp312-win_amd64.whl</td>
</tr>
</tbody>
</table>

2\. **项目代码**

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr>
<td style="text-align: left;">Shell<br />
|- lerobot<br />
|- configs # 程序运行配置文件目录<br />
|- src # 源码目录<br />
|- lerobot<br />
|- libs # 工具包，如usb管理工具</td>
</tr>
</tbody>
</table>

3\. **机械臂校准**

目的：通过机械臂校准，可以将机械臂舵机角度标准化到固定空间，便于不同机械臂间的操作同步和模型同步。

**3.1 USB绑定**

目的：通过USB绑定，可以避免插拔USB导致端口变化而频繁修改配置参数。

操作方式：管理员运行打开libs/usbdeview/USBDeview.exe

**> 附：视频文件「20251202_184743.mp4」，请在 GitBook 中手动上传该文件。**

根据上述方法依次对机械臂和摄像头进行端口绑定，其中机械臂端口命名为robot，机械臂手肘部摄像头命令为wrist。

**3.2 校准**

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr>
<td style="text-align: left;">Shell<br />
# 修改calibrate.yaml参数后运行<br />
lerobot-calibrate.exe --config_path=configs/calibrate.yaml</td>
</tr>
</tbody>
</table>

详细参数：

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr>
<td style="text-align: left;">YAML<br />
robot:<br />
type: sam01_follower # 机械臂类型，无需修改<br />
id: robot_arm_follower # 机械臂ID, 可修改，与校准文件名称相关<br />
port: robot # 左侧从臂COM口名称<br />
cameras: {} # 摄像头参数，为空表示校准时不考虑摄像头<br />
calibration_dir: C:/ai02pro/user_data/test/lerobot_calibration # 校准文件目录</td>
</tr>
</tbody>
</table>

校准参考示例：（补充视频）

4\. **遥操作**

目前提供键盘和手柄两种遥操作方式。

键盘控制按键：

|          |              |
|:---------|:-------------|
| **按键** | **功能**     |
| w        | 向前移动     |
| s        | 向后移动     |
| a        | 向左移动     |
| d        | 向右移动     |
| q        | 升高         |
| e        | 降低         |
| r        | 打开夹爪     |
| f        | 关闭夹爪     |
| y        | 末端向左旋转 |
| u        | 末端向右旋转 |
| h        | 抬头         |
| j        | 低头         |
| n        | 左偏         |
| m        | 右偏         |

手柄控制按键：使用 罗技标准手柄，**使用前请确认手柄控制模式为D（Direct），MODE指示灯为熄灭状态**

|  |  |
|:--:|:--:|
| ![AI02pro模仿学习实验指导书_assets/media/image1.png](AI02pro模仿学习实验指导书_assets/media/image1.png) | ![AI02pro模仿学习实验指导书_assets/media/image2.png](AI02pro模仿学习实验指导书_assets/media/image2.png) |

|          |                              |
|:---------|:-----------------------------|
| **按键** | **功能**                     |
| 左摇杆   | 上下左右分别控制前后左右移动 |
| 右摇杆   | 上下分别控制升高和降低       |
| 上方向键 | 抬头                         |
| 下方向键 | 低头                         |
| 左方向键 | 左偏                         |
| 有方向键 | 右偏                         |
| LB       | 末端向左旋转                 |
| RB       | 末端向右旋转                 |
| LT       | 打开夹爪                     |
| RT       | 关闭夹爪                     |

遥操作前需要确定机械臂的运动空间，避免碰撞，运行如下命令：

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr>
<td style="text-align: left;">Shell<br />
lerobot-find-joint-limits.exe --config_path=configs/find_joint_limits.yaml</td>
</tr>
</tbody>
</table>

启动后，拖动机械臂在设定的空间内移动，移动完成后按下ESC停止程序，将打印如下内容：

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr>
<td style="text-align: left;">Shell<br />
Max ee position [0.3154, 0.147, 0.4375]<br />
Min ee position [-0.0376, -0.2263, 0.0525]<br />
Max joint pos position [59.8535, 98.2497, 59.9807, 6.0078, 7.4555, 68.4005, 93.6438]<br />
Min joint pos position [-45.4945, -59.4657, -98.2642, -88.1783, -20.9235, -4.6642, 92.8307]</td>
</tr>
</tbody>
</table>

将上述最大和最小的ee position（末端位姿）替换teleoperate.yaml中的默认参数：

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr>
<td style="text-align: left;">YAML<br />
# 末端控制边界保护<br />
- name: ee_bounds_and_safety<br />
end_effector_bounds: # 位置边界<br />
min: [0, -0.23, 0.03]<br />
max: [0.25, 0.1, 0.15]<br />
max_ee_step_m: 0.2 # 单次移动最大距离，米</td>
</tr>
</tbody>
</table>

遥操作运行命令：

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr>
<td style="text-align: left;">Shell<br />
lerobot-teleoperate.exe --config_path=configs/teleoperate.yaml</td>
</tr>
</tbody>
</table>

详细参数：

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr>
<td style="text-align: left;">YAML<br />
robot:<br />
type: sam01_follower<br />
id: robot_arm_follower<br />
port: robot<br />
calibration_dir: C:/ai02pro/user_data/test/lerobot_calibration # 校准文件目录<br />
cameras:<br />
high:<br />
type: orbbec<br />
width: 640<br />
height: 480<br />
fps: 30<br />
# wrist:<br />
# type: opencv<br />
# index_or_path: wrist<br />
# width: 640<br />
# height: 480<br />
# fps: 30<br />
teleop:<br />
type: gamepad # 遥操作方式：手柄(gamepad)、键盘（keyboard_ee）<br />
use_gripper: true<br />
<br />
processor:<br />
robot_action_steps:<br />
# delta移动坐标转换成机械臂控制指令<br />
- name: map_delta_action_to_robot_action<br />
<br />
# 转换成末端控制<br />
- name: ee_reference_and_delta<br />
kinematics_config: &amp;kc<br />
urdf_path: C:/ai02pro/project/lerobot/assets/sam01_robot_left/sam01_robot.xml # URDF文件路径，xml或URDF<br />
target_frame_name: joint6 # 末端关节名称<br />
last_joint_as_gripper: true # 最后一个关节是否时夹爪<br />
last_joint_name: joint7 # 最后一个关节是否为夹爪，last_joint_as_gripper为真时设置<br />
position_weight: 20.0 # 逆解位置权重<br />
rotation_weight: 1 # 逆解旋转权重<br />
end_effector_step_sizes: # 末端步幅<br />
x: 0.002<br />
y: 0.002<br />
z: 0.002<br />
roll: 1 # 旋转<br />
pitch: 1 # 俯仰角<br />
yaw: 1 # 偏航角<br />
motor_names: &amp;mn ["shoulder_pan","shoulder_lift","elbow_flex","wrist_flex","forearm_roll","wrist_roll","gripper"]<br />
use_latched_reference: true<br />
rpy_joint_index_map:<br />
roll: 5<br />
pitch: 3<br />
yaw: 4<br />
<br />
# 末端控制边界保护<br />
- name: ee_bounds_and_safety<br />
end_effector_bounds: # 位置边界<br />
min: [0, -0.23, 0.03]<br />
max: [0.25, 0.1, 0.15]<br />
max_ee_step_m: 0.2 # 单次移动最大距离，米<br />
<br />
# 夹爪速度转化成角度<br />
- name: gripper_velocity_to_joint<br />
clip_max: 100 # 最大值<br />
clip_min: 0 # 最小值<br />
speed_factor: 1.0 # 速度系数<br />
discrete_gripper: true # 是否离散化到[-1, 0, 1]<br />
<br />
# 末端控制转换关节角度<br />
- name: inverse_kinematics_ee_to_joints<br />
kinematics_config: *kc<br />
motor_names: *mn<br />
initial_guess_current_joints: true # 使用当前关节角作为初始值<br />
<br />
display_data: true</td>
</tr>
</tbody>
</table>

5\. **数据采集**

运行命令：

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr>
<td style="text-align: left;">Shell<br />
lerobot-record.exe --config_path=configs/record_dataset.yaml</td>
</tr>
</tbody>
</table>

详细参数：

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr>
<td style="text-align: left;">YAML<br />
robot:<br />
type: sam01_follower<br />
id: robot_arm_follower<br />
port: robot<br />
calibration_dir: C:/ai02pro/user_data/test/lerobot_calibration # 校准文件目录<br />
cameras:<br />
high:<br />
type: orbbec<br />
width: 640<br />
height: 480<br />
fps: 30<br />
# wrist:<br />
# type: opencv<br />
# index_or_path: wrist<br />
# width: 640<br />
# height: 480<br />
# fps: 30<br />
teleop:<br />
type: gamepad<br />
use_gripper: true<br />
<br />
processor:<br />
# 遥操作指令处理步骤<br />
teleop_action_steps:<br />
# delta移动坐标转换成机械臂控制指令<br />
- name: map_delta_action_to_robot_action<br />
<br />
# 转换成末端控制<br />
- name: ee_reference_and_delta<br />
kinematics_config: &amp;kc # 运动学参数<br />
urdf_path: C:/ai02pro/project/lerobot/assets/sam01_robot_left/sam01_robot.xml # URDF文件路径，xml或URDF<br />
target_frame_name: joint6 # 末端关节名称<br />
last_joint_as_gripper: true # 最后一个关节是否时夹爪<br />
last_joint_name: joint7 # 最后一个关节是否为夹爪，last_joint_as_gripper为真时设置<br />
position_weight: 20.0 # 逆解位置权重<br />
rotation_weight: 1 # 逆解旋转权重<br />
end_effector_step_sizes: # 末端步幅<br />
x: 0.002<br />
y: 0.002<br />
z: 0.002<br />
roll: 1 # 旋转<br />
pitch: 1 # 俯仰角<br />
yaw: 1 # 偏航角<br />
motor_names: &amp;mn ["shoulder_pan","shoulder_lift","elbow_flex","wrist_flex","forearm_roll","wrist_roll","gripper"]<br />
rpy_joint_index_map: # RPY角度与关节映射<br />
roll: 5 # 映射到第6个关节<br />
pitch: 3 # 映射到第4个关节<br />
yaw: 4 # 映射到第5个关节<br />
<br />
# 末端控制边界保护<br />
- name: ee_bounds_and_safety<br />
end_effector_bounds: # 位置边界<br />
min: [0, -0.23, 0.03]<br />
max: [0.25, 0.1, 0.15]<br />
max_ee_step_m: 0.2 # 单次移动最大距离，米<br />
<br />
# 夹爪速度转成角度<br />
- name: gripper_velocity_to_joint<br />
clip_max: 100 # 最大值<br />
clip_min: 0 # 最小值<br />
speed_factor: 1.0 # 速度系数<br />
discrete_gripper: true # 是否离散化到[-1, 0, 1]<br />
<br />
# 机械臂指令处理步骤<br />
robot_action_steps:<br />
# 末端控制转换关节角度<br />
- name: inverse_kinematics_ee_to_joints<br />
kinematics_config: *kc<br />
motor_names: *mn<br />
initial_guess_current_joints: true # 使用当前关节角作为初始值<br />
<br />
# 机械臂观测处理步骤<br />
robot_observation_steps:<br />
# 机械臂关节角转换为EE末端<br />
- name: forward_kinematics_joints_to_ee<br />
kinematics_config: *kc<br />
motor_names: *mn<br />
<br />
dataset:<br />
root: C:/ai02pro/user_data/test/lerobot_datasets # 数据集根目录<br />
repo_id: test/fenjian_test_1 # 数据集名称<br />
single_task: 桌面分拣 # 数据集描述<br />
fps: 30 # 帧率<br />
episode_time_s: 60 # 视频最大时长<br />
reset_time_s: 10 # 重置时间<br />
num_episodes: 10 # 数据集数量<br />
tags: ["sam","tutorial"] # 标签<br />
push_to_hub: false # 是否推送到huggingface<br />
<br />
display_data: true # 是否显示数据<br />
resume: false # 是否继续录制</td>
</tr>
</tbody>
</table>

6\. **数据回放**

完成数据采集后，可以回放机械臂的轨迹路径。

运行命令：

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr>
<td style="text-align: left;">Shell<br />
lerobot-replay.exe --config_path=configs/replay.yaml</td>
</tr>
</tbody>
</table>

7\. **数据集可视化**

运行命令：

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr>
<td style="text-align: left;">Shell<br />
lerobot-replay.exe --config_path=configs/replay.yaml</td>
</tr>
</tbody>
</table>

详细参数：

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr>
<td style="text-align: left;">Shell<br />
repo_id: test/fenjian_test_1<br />
root: C:/ai02pro/user_data/test/lerobot_datasets</td>
</tr>
</tbody>
</table>

结果示例：（补充图片）

8\. **模型训练**

运行命令：

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr>
<td style="text-align: left;">Shell<br />
lerobot-train.exe --config_path=configs/train_act.yaml</td>
</tr>
</tbody>
</table>

详细参数：

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr>
<td style="text-align: left;">YAML<br />
dataset:<br />
repo_id: test/fenjian_test_1<br />
root: C:/ai02pro/user_data/test/lerobot_datasets<br />
image_transforms:<br />
enable: false # 是否开启图像增强<br />
# episodes: [0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19] # 训练的视频索引序列<br />
<br />
policy:<br />
type: act # 策略类型<br />
vision_backbone: resnet18 # 视觉骨干网络名称<br />
pretrained_backbone_weights: ResNet18_Weights.IMAGENET1K_V1 # 预训练权重名称<br />
backbone_per_camera: false # 是否每个摄像头使用不同骨干网络<br />
chunk_size: 100 # 行为块大小<br />
kl_weight: 50.0 # KL散度损失权重系数<br />
optimizer_lr: 1e-5 # 学习率<br />
optimizer_lr_backbone: 1e-5 # 骨干网络学习率<br />
optimizer_weight_decay: 1e-4 # 权重衰减<br />
use_amp: true # 是否使用混合精度训练<br />
push_to_hub: false # 是否推送到huggingface<br />
use_vae: true # 是否使用VAE编码器<br />
<br />
output_dir: C:/ai02pro/user_data/test/lerobot_trained_models/act_fenjian_test1 # 输出文件夹<br />
job_name: act_fenjian_test1 # 任务名称<br />
batch_size: 8 # 批次大小<br />
steps: 30000 # 总步数<br />
save_freq: 10000 # 保存间隔<br />
num_workers: 6 # 数据加载线程数</td>
</tr>
</tbody>
</table>

9\. **模型测试**

运行命令：

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr>
<td style="text-align: left;">Shell<br />
lerobot-test.exe --config_path=configs/test_policy.yaml</td>
</tr>
</tbody>
</table>

详细参数：

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr>
<td style="text-align: left;">YAML<br />
robot:<br />
type: sam01_follower<br />
id: robot_arm_follower<br />
port: robot<br />
calibration_dir: C:/ai02pro/user_data/test/lerobot_calibration # 校准文件目录<br />
cameras:<br />
high:<br />
type: orbbec<br />
width: 640<br />
height: 480<br />
fps: 30<br />
# wrist:<br />
# type: opencv<br />
# index_or_path: wrist<br />
# width: 640<br />
# height: 480<br />
# fps: 30<br />
policy:<br />
type: act # 策略类型<br />
n_action_steps: 100 # act参数，单次预测执行的步数<br />
device: cuda<br />
<br />
processor:<br />
# 机械臂指令处理步骤<br />
robot_action_steps:<br />
# 末端控制转换关节角度<br />
- name: inverse_kinematics_ee_to_joints<br />
kinematics_config: &amp;kc<br />
urdf_path: C:/ai02pro/project/lerobot/assets/sam01_robot_left/sam01_robot.xml<br />
target_frame_name: joint6<br />
last_joint_as_gripper: true<br />
last_joint_name: joint7<br />
position_weight: 20.0<br />
rotation_weight: 1<br />
motor_names: &amp;mn ["shoulder_pan","shoulder_lift","elbow_flex","wrist_flex","forearm_roll","wrist_roll","gripper"]<br />
initial_guess_current_joints: true<br />
<br />
# 机械臂观测处理步骤<br />
robot_observation_steps:<br />
# 机械臂关节角转换为EE末端<br />
- name: forward_kinematics_joints_to_ee<br />
kinematics_config: *kc<br />
motor_names: *mn<br />
<br />
task: # 任务描述<br />
inference_time_s: 300 # 推理时长<br />
fps: 30 # 帧率<br />
pretrained_name_or_path: C:/ai02pro/user_data/test/lerobot_trained_models/act_fenjian_test1/checkpoints/last/pretrained_model</td>
</tr>
</tbody>
</table>
