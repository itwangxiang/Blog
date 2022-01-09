# ADB 常用命令


### 常规
  
```bash
adb tcpip 5555 //设置远程设备监听端口
adb connect ip:port //连接远程设备
adb -s 20b5c60c shell ifconfig wlan0 //查看 IP
adb reconnect //重新连接设备
adb shell am start -n ｛package｝/.{activity} //启动程序
adb shell setprop persist.service.adb.tcp.port 5555 //设置系统重启后，远程设备监听端口
adb shell wifitest -z "W 00:1f:2e:3d:4c:5b" //设置 WI-FI MAC
adb shell wifitest -z "B 00:1f:2e:3d:4c:5b" //设置 蓝牙 MAC
```
