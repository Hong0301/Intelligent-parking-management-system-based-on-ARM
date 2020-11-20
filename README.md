# Intelligent-parking-management-system-based-on-ARM
项目实现：
1：使用RFID打卡作为入场和出场识别。 
   (刷第一次查询数据库是否该卡号，没有就是进场，有就是出场)
   进场：记录进场的时间，卡号，进场的车辆照片（v4l2编程）  
   出场：计费，显示当时进场的车辆照片，从数据库中删除该车辆的信息  
2：使用数据库进行车位管理。  
     （可以人为修改车辆在数据库中的信息，假设是VIP卡则需要计费）
3：实时监控出入口视频。 （V4L2编程，利用一个线程不断采集摄像头的数据并显示）   
4：实现语音播报车辆信息与消费信息。（车场就播报车辆的卡信息，出场就播报消费金额）

5：添加管理员功能。

项目具体需求：
1： 创建一个数据库， 内置你需要的所有信息, 如车牌信息、RFID卡信息、卡类、进场时间、车辆照片名等
2： 在默认状态下，视频监控是处于打开状态的，并循环录制，1分钟视频，保存到本地。
当检测到有RFID卡，关闭视频流，判断当前数据库中是否有该卡的入场信息：
1）如果已有该卡的入场信息，表示现在是出场；则直接计算出当前时间和入场时间差值，在屏幕上显示该车辆照片，显示车辆信息和应收费金额
2）如果没有该卡的入场信息，则在数据库中增加该车辆信息，并记录当前时间且拍照。
3）在检测到RFID卡3秒后， 系统会恢复打开视频流

4:当车辆刷卡进场是，语音提示卡号，并说明卡的类别（临时卡，或包月卡），出场提示：费用与月卡剩余天数
5：管理功能，负责把卡的类别进行修改，与数据库中的数据进行修改。
6:  自行扩展： 添加一些自主功能。
