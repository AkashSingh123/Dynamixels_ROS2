# Dynamixels_ROS2
ROS2_Dynamixel
mkdir -p ~/ros2_workspace/src
cd ~/ros2_workspace

import rclpy
from rclpy.node import Node
from dynamixel_sdk import *
import time

class SnakeRobotControl(Node):
    def __init__(self):
        super().__init__('snake_robot_control')
        port = PortHandler(DEVICE_NAME)
        packet_handler = PacketHandler(PROTOCOL_VERSION)
        port.openPort(COM5)
        port.setBaudRate(BAUDRATE)
        dynamixel = Dynamixel(COM5, packet_handler, DX_12)
        dynamixel.setOperatingMode(POsition_Control)
        dynamixel.setGoalPosition(360)

def main(args=None):
    rclpy.init(args=args)
    node = SnakeRobotControl()
    rclpy.spin(node)
    node.destroy_node()
    rclpy.shutdown()

if __name__ == '__main__':
    main()
