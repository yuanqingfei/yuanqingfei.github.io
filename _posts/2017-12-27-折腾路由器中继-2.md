---
published: true
categories: technique
tags: router repeater
---
山重水复疑无路，柳暗花明又一村。

昨天刚刚[夸奖了DD-WRT](https://yuanqingfei.me/technique/%E6%8A%98%E8%85%BE%E8%B7%AF%E7%94%B1%E5%99%A8%E4%B8%AD%E7%BB%A7/)，结果文章写完后回去一看，我去，又上不去无线网络了，这稳定性也太差了，于是继续折腾。

## 尝试OpenWrt
本来是打算根据youtube上的[这个视频](https://www.youtube.com/watch?v=1vsPz_aLZeE)来设置一下的。结果等我把firmare刷上了，才明白[关于设备E3200页面](https://wiki.openwrt.org/toh/linksys/e3200)上面那个大大的惊叹号的意思。我去，这货根本不支持E3200wifi功能，这还怎么玩。 
![openwrt.png]({{site.baseurl}}/images/openwrt.png)

思前想后，继续搜索，才知道人家Tomato虽然没有repeator的选项，其实还是可以做repeator或者repeator bridge的功能的，之前学习太肤浅了，检讨。可是怎么才能刷回Tomato的firmware呢。在OpenWrt的界面上，说Tomato的固件不兼容，不能通过GUI来刷。必须通过WinSCP连接上再用 mtd -r **-f** write /tmp/tomato.bin firmware 来刷。 具体，请参考[这个视频](https://www.youtube.com/watch?v=ofXUtkj5d24)。 

## 重归Tomato
重新看了下Tomato的[wiki](https://en.wikipedia.org/wiki/Tomato_(firmware))，发现现在一直比较活跃并且在维护的版本分别是：[Tomato by Shibby](http://tomato.groov.pl)， [AdvancedTomato](https://advancedtomato.com)以及[kille72](https://bitbucket.org/kille72/tomato-arm-kille72)。根据论坛上的指示，Shibby版本口碑不错，就它了，而且到了它的各种型号[支持页面](http://tomato.groov.pl/?page_id=69)一看，我的E3200在其中。赶紧就刷上去了，然后就根据一个[菲律宾小伙的具体步骤](https://www.spideylab.com/tomato-router-wireless-repeater-ethernet-bridge-mode/)搞定。
摘录如下：
>1. Access the Gateway of the Tomato (second router) and navigate to Advanced Settings > Virtual Wireless.
>2. Add new interface (wl0.1) and SSID (name) according to your liking. Set the mode to Access Point and bridge to LAN (br0). Click Add then Save. Note: This setup is  crucial as you will not be able to connect to the second router wirelessly when this is not done.
>3. Navigate to Basic Settings > Network.
>4. Go to the category LAN and edit the values. Set the IP address to 192.168.1.2, subnet mask 255.255.255.0 and disable DHCP.
>5. Right beneath the LAN settings, input 192.168.1.1 as the Default Gateway and DNS. Note: The Default Gateway option is somehow tricky and it may not appear until you save the changes. If it is missing, just proceed to Step 6.
>6. Go to Wireless (eth1) category. Change the Wireless mode to Wireless Ethernet Bridge.
>7. Input the WiFi SSID and password of the primary router.  Configure the correct wireless network and encryption mode the same values you have in the primary router. Hit Save. (The Default Gateway setting should now appear and configure it with the value in Step 5. Hit save again.)
>8. Navigate to Advanced Settings > Routing.
>9. Go to the Miscellaneous category. Make sure the mode is set to Gateway, RIPv1 & V2 disabled and DHCP routes is checked. Save. The DHCP routes is important as it is the way to send all DHCP requests to the primary router (DHCP server).
>10. Navigate to Advanced Settings > Firewall.
>11. Go to category NAT and set the NAT loopback to Forwarded Only. Checked Enable SYN cookies. Save. (NAT Loopback: This setting is crucial as you may experience connection problems/unstable router when it is set to All.)

这个模式其实是repeater bridge模式，是在同一个网段的，本来我是打算做成repeator模式的，这次图省事，就算了，有空再折腾吧。喜欢自己尝试的朋友可以试试Tomato上面的试试是否真的可以repeator。 bridge模式已经上线2个多小时了，比较稳定。可堪一用。
![TomatoRouter.JPG]({{site.baseurl}}/images/TomatoRouter.JPG)
