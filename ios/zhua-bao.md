iPhone通过usb连接macbook时，Wireshark并不能直接监听通过iPhone的网络流量，需要建立一个映射到iPhone的虚拟网卡。

在terminal中输入如下命令即可：

```
// rvictl -s [设备udid]
rvictl -s C6B504C655438EEA6C9FD1A113C44D2914C22999
```

设备udid，通过itunes在【摘要】页，可以看到设备的序列号，点击【序列号】可以得到。

执行命令之后Wireshark能立即识别新增加的rvi0网卡。



```
/**
 * Capture Filter的规则
 */

//只捕获HTTP流量
port 80 or port 443

//只捕获DNS流量
port 53

//只捕获和特定主机的流量
host 171.10.191.10
```



```
/**
 * Display Filter的语法是由Wireshark自定义
 */
 
// 只看某个主机的流量 
ip.addr==171.10.191.10

// 只看http或者https的流量
tcp.port == 80 || tcp.port == 443
```

更多的语法规则可以查看

[Wireshark官方文档](https://www.wireshark.org/docs/wsug_html_chunked/ChWorkBuildDisplayFilterSection.html)

https://www.wireshark.org/docs/wsug\_html\_chunked/ChWorkBuildDisplayFilterSection.html

Wireshark实际上提供了便捷的UI操作帮助我们来书写Display Filter，在Display Filter输入框的最右边有个Expression按钮，点击之后可以弹出界面

### 包颜色规则

具体的规则可以通过菜单View-&gt;Coloring Rules...查看

只将我感兴趣的协议包上了色，集中在http，tcp，udp包，这样分析起来更加直观。

比如tcp三次握手中的Sync包是使用灰色标记的，这样就可以迅速定位一次tcp连接的开始包位置

### 流量跟踪

##### 方式一：Follow Stream

当我们选中某个包之后，右键弹出的菜单里，有个选项允许我们将当前包所属于的完整流量单独列出来

##### 方式二：Flow Graph

Flow Graph可以通过菜单Statistics-&gt;Flow Graph来生成，这样我们可以得到另一种形式的流量呈现

Follow Stream更适合分析针对某一个服务器地址的流量，而Flow Graph更适合分析某个App的整体网络行为，包含从DNS解析开始到和多个服务器交互等。

其实Statistics菜单下还有更多的图表分析模式，可以根据不同的分析目标来选择，比如Statistics-&gt;HTTP-&gt;Requests可以得到如下按主机分门别类的HTTP请求分析图



