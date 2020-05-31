---
title:      "Juniper防火墙设置地址映射"
cover:      "https://image.123m.me/images/2019/02/02/38b3e9c0ea581028e1d5cce8bd1ed3fe.md.png"
date:       "2019-02-01 14:14:33"
tags:
    - 网络
---

Juniper防火墙做端口映射功能，所有操作都是在web管理界面进行操作：  
1. 选择菜单Policy > Policy Elements > Services > Custom，进入自定义服务管理页面  
![fa5e0d9278e6f351b446696caedb9ebb.jpg](https://image.123m.me/images/2019/02/11/fa5e0d9278e6f351b446696caedb9ebb.jpg)

2. 点击右上角的New按钮进入自定义服务添加页面  
![002218ea3d5f8ff8f9fd722528540b1f.jpg](https://image.123m.me/images/2019/02/11/002218ea3d5f8ff8f9fd722528540b1f.jpg) 
在Service Name处填写自定义的服务名称，在Transport protocol处选择需要使用的协议，在Destination
Port 处填写自定义服务的目的端口，点击OK按钮提交操作。在上图中，我们添加了了一个名为udp-3311的服务，它使用UDP协议，目的端口号为3311。  

3. 选择菜单Network > Interfaces(List)，找到Untrust Zone对应的端口名（图中Untrust Zone对应的端口为ethernet0/0），点击右边的Edit按钮进入端口编辑页面  
![2e339ac0b98e38e3572c83929ad2b62e.jpg](https://image.123m.me/images/2019/02/11/2e339ac0b98e38e3572c83929ad2b62e.jpg)

4. 点击Properties中的VIP按钮，切换到VIP管理页面  
![5e8332343977cf8f831f463a18465e17.jpg](https://image.123m.me/images/2019/02/11/5e8332343977cf8f831f463a18465e17.jpg)
初次添加VIP设置时，如果你有多个外网IP地址，你可以选择填入你的Virtual IP Address，如果ISP只提供给你一个外网IP地址或者你通过PPPOE方式获得外网IP，你可以选择Same as the untrusted interface IP address，点击Add按钮提交。

5. 点击New VIP Service按钮，进入VIP服务添加页面
![901447bb639b1774d8a80a14d668b18e.jpg](https://image.123m.me/images/2019/02/11/901447bb639b1774d8a80a14d668b18e.jpg)

6. 添加VIP Service相关信息  
A、在Map to Service 下拉列表中选择现有服务类型或者自定义的服务，图中我们选择了之前添加的udp-3311服务  
B、在Map to IP中填写提供服务的主机IP，Virtual Port与自定义服务的端口一致，不要勾选Server Auto Detection后Enable选项,点击OK按钮提交  
![0b854b4faa6c6eea395f3a6c3b5b73b2.jpg](https://image.123m.me/images/2019/02/11/0b854b4faa6c6eea395f3a6c3b5b73b2.jpg)

7. 选择菜单Policy > Policies,进入策略管理页面
![418d10fef776cbac7003708b6f380766.jpg](https://image.123m.me/images/2019/02/11/418d10fef776cbac7003708b6f380766.jpg)

8. 左上角的From选择Untrust Zone，To选择Trust Zone，点击NEW进入From Untrust To Trust策略新增页面
![da0d8c1879b92fc77cca9b0e08803fd7.jpg](https://image.123m.me/images/2019/02/11/da0d8c1879b92fc77cca9b0e08803fd7.jpg)
Source Address（源地址）从Address Book Entry中选择Any;Destination Address（目的地址）从Address Book Entry中选择相关的VIP服务，Service选择自定义的服务。图中目的地址我们选择了之前添加的VIP(ethernet0/0)，Service选择之前自定义的udp-3311服务，完成后，点击OK按钮提交。  
至此，端口映射就完成了，如需添加多个端口映射，方法类似。
