# 通信协议

采用串行通信（TTL）：

波特率：115200

## 1、发送数据

ROS ---->底盘

需实现两个电机独立闭环控制

最高发送频率：20HZ

| Byte | Signal | type     | Describe |
| ---- | ------ | -------- | -------- |
| 0    | 帧头   | unsigned | 固定值，0xa5 |
| 1    | 帧头   | unsigned | 固定值，0x5a |
| 2 | LEN | unsigned | sizeof（DATA） |
| 3  | 左轮速度   | signed | 高字节   |
| 4 | 左轮速度 | signed | 低字节 |
| 5  | 右轮速度   | signed | 高字节   |
| 6 | 右轮速度 | signed | 低字节 |
| 7 | 车体宽度变化   | unsigned | ？？？0，无动作；1，伸展 |
| 8  | SUM   | unsigned | 累加和校验   |

> 问号处：不确定是否只有两个状态
>
> 累积和：sum(byte[2-26])

## 2、接收数据

底盘 ---->ROS

发送频率：暂定 20HZ

| Byte | Signal | type     | Describe |
| ---- | ------ | -------- | -------- |
| 0    | 帧头   | unsigned | 固定值，0xa5 |
| 1    | 帧头   | unsigned | 固定值，0x5a |
| 2 | LEN | unsigned | sizeof（DATA） |
| 3  | 左编码器增量   | signed | 高字节   |
| 4 | 左编码器增量 | signed | 低字节 |
| 5  | 右编码器增量   | signed | 高字节   |
| 6 | 右编码器增量 | signed | 低字节 |
| 7 | 车体宽度   | unsigned | ？？？0，未伸展；1，未伸展 |
| 8  | GYRO.X   | signed | X轴角速度高字节   |
| 9 | GYRO.X | signed | X轴角速度低字节 |
| 10  | GYRO.Y   | signed | Y轴角速度高字节   |
| 11 | GYRO.Y | signed | Y轴角速度低字节 |
| 12 | GYRO.Z   | signed | Z轴角速度高字节   |
| 13 | GYRO.Z | signed | Z轴角速度低字节 |
| 14  | ACCEL.X   | signed | X轴线加速度高字节   |
| 15 | ACCEL.X | signed | X轴线加速度低字节 |
| 16  | ACCEL.Y   | signed | Y轴线加速度高字节   |
| 17 | ACCEL.Y | signed | Y轴线加速度低字节 |
| 18 | ACCEL.Z   | signed | Z线加角速度高字节   |
| 19 | ACCEL.Z | signed | Z轴线加速度低字节 |
| 20  | MAG.X   | signed | X轴磁力计数据高字节   |
| 21 | MAG.X | signed | X轴磁力计数据低字节 |
| 22  | MAG.Y   | signed | Y轴磁力计数据高字节   |
| 23 | MAG.Y | signed | Y轴磁力计数据低字节 |
| 24 |MAG.Z   | signed | Z磁力计数据度高字节   |
| 25 | MAG.Z | signed | Z轴磁力计数据低字节 |
| 26 | RFID | unsigned | RFID数据 |
| 27 | SUM | unsigned |累加和校验 |







