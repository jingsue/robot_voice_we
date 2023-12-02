# robot_voice_ws
# 该包是基于科大讯飞实时语音听写，将SDK集成到ROS2包中
# 包的名称robot_voice 节点的名称voice_node
# 致谢 感谢卢师哥、大涵哥、超哥的帮助完成ROS2的集成

# 使用
# 找到CMakeLists.txt 修改里面的set(SRC /home/llt/robot_voice_test_ws/src)，将llt改为自己的设备的名称
# 在robot_voice_ws下删除掉install、log、ms以及bulid文件
# 在robot_voice_ws下执行终端 输入colcon build --packages-select robot_voice。
# 执行source install/setup.bash
# 执行ros2 run robot_voice voice_node
