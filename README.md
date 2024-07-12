# 📝davinci resolve project server一些已知使用问题整理
>重点解决两个问题：  
1、解决达芬奇更换路由后协同作业时nas能直连但是协同服务器连不上。  
2、postgresql在达芬奇协同中启动后自动关闭的问题。
***
## ❓问题一：更换路由后，达芬奇协同作业时nas能直连但是协同服务器连不上：
>* 大概率时没有给[5432]端口建立入站规则原因导致。
### 🔅解决方案
#### 给【5432】端口设立入站规则
1、打开控制面板（WIN+R打开运行程序，输入Control ）  
2、打开【管理工具】，双击打开【高级安全 Windows Defender 防火墙”】  
3、右键【入站规则】 - 【新建规则】  
4、选择端口 - 输入【5432】  
5、规则默认【tcp】  
6、自己命名个名称，点击完成【完成】即可  
#### 检查PostgreSQL文件夹下的pg_hba文件中的ip地址和名称是否一致  
1、打开
```Bash
PostgreSQL\12\data
```
2、找到pg_hba文件，右键打开方式选择记事本  
3、查看最下面-【me2023】对应【名称】；【192.168.0.125】对应【位置】；确认IP信息是否是一致。 
***
## ❓问题二：postgresql在达芬奇协同中启动后自动关闭：在等待服务器超时
### 🔅解决方案
1、打开
```Bash
PostgreSQL\12\Bin
``` 
2、输入命令 
```Bash
.\pg_resetwal.exe -f ..\data （重写日志）
```
3、输入命令 
```Bash
.\pg_ctl start -D ..\data （重启服务器）
```
4、解决问题

## 📍其他已知问题
[达芬奇数据库不显示](https://zhuanlan.zhihu.com/p/398936161#:~:text=%E5%A6%82%E6%9E%9C%E4%BD%A0%E7%9A%84%E9%A1%B9%E7%9B%AE%E6%B2%A1%E6%9C%89%E6%98%BE%E7%A4%BA%EF%BC%8C%E9%82%A3%E4%B9%88%E8%AF%B7%E5%8F%B3%E5%87%BB%E7%A9%BA%E7%99%BD%E5%A4%84%E7%82%B9%E5%87%BB%22%E5%88%B7%E6%96%B0%22%E3%80%82,%E8%BF%99%E6%A0%B7%EF%BC%8C%E8%BE%BE%E8%8A%AC%E5%A5%87%E7%9A%84%E9%A1%B9%E7%9B%AE%E7%AE%A1%E7%90%86%E5%99%A8%E5%B0%B1%E4%BC%9A%E6%98%BE%E7%A4%BA%E4%BD%A0%E6%81%A2%E5%A4%8D%E7%9A%84%E9%A1%B9%E7%9B%AE%E3%80%82)  
[达芬奇数据库崩溃后重启教程](https://blog.csdn.net/my_name_nb/article/details/85237718)
