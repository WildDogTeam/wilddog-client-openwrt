
####wilddog-client-openwrt说明：

`wilddog-client-openwrt` 提供了一整套访问和操作野狗云端数据的 API，用户只需要在 OpenWRT 上安装，即可在应用中调用野狗提供的 API 访问野狗云端的数据.

#####1. 下载

从git下载到文件夹

	git clone https://github.com/WildDogTeam/wilddog-client-openwrt.git

#####2. 部署到 OpenWRT 项目中
将`wilddog-client-openwrt/tools/libwilddog`文件夹拷贝到 OpenWRT 项目中的`package/libs/`目录下.

	cp -rf wilddog-client-openwrt/tools/libwilddog  <your openwrt path>/package/libs/

#####3. 在 OpenWRT 项目下制作 ipk 并安装

1. 在 OpenWRT 项目的根目录下运行`make menuconfig`；

2. 在`Libraries`目录下，选中`libwilddog`，并设置为 module（如果设置为built-in，则可忽略3、4两步,但需要将整个openwrt固件刷到设备中);

		{M} libwilddog........................................ A Library for real-time commuication.

3. 运行 make，编译OpenWRT；

4. 编译成功后，在`bin`目录下能找到`libwilddog_x.x.x-x_xxxx.ipk`；

5. 将这个 ipk 上传到 OpenWRT 中，并使用 opkg 命令安装

		opkg install libwilddog_x.x.x-x_xxxx.ipk


#####4. 范例使用

1. 将`wilddog-client-openwrt/examples/demo`文件夹（以及其中的`Makefile`文件）拷贝到 OpenWRT 项目中的`package/utils/`目录下.

	 	cp -rf wilddog-client-openwrt/examples/demo  <your OpenWRT project path>/package/utils/

2. 配置，生成`demo.ipk`，执行`make menuconfig`，在`Utilities`选中`demo`，并设置为`module`模式;
	
		<M> demo............................ demo -- demo show how to use libwilddog 

3. 编译：

		make V=s

4. 将编译出来的`bin`目录下的`demo_x_xxxx.ipk`上传到 OpenWRT 中，并使用 opkg 命令安装;

		opkg install demo_x_xxxx.ipk

5. 使用 demo 获取数据:

		demo getValue -l coap://<appId>.wilddogio.com/YourPath 

	`<appId>`为在野狗上申请的应用名称.

6. 该 demo 展示了如何获取、更新、删除野狗云端数据，具体使用请阅读源码.
		
#####5. 高级配置

可以在`wilddog-client-openwrt/tools/libwilddog`目录下的 Makefile 中对 SDK 进行配置。

	define Build/Configure
 	 $(call Build/Configure/Default,--with-endian=big)
	endef

在这里，可以在`$(call Build/Configure/Default,--with-endian=big)`中增加配置项：

	--with-endian=ARG       大小端, ARG可设为big|little,  默认little
	--with-bits=ARG         机器位数, ARG可设为8|16|32|64, 默认32
	--with-maxsize=ARG      应用层协议长度, ARG可设为0~1300, 默认1280
	--with-queuenum=ARG     消息队列个数, 默认32
	--with-retranstime=ARG  重传超时时间（ms）, 默认10000ms
	--with-recvtimeout=ARG  单次最大接收时间（ms）, 默认100ms
	--with-sectype=ARG      加密方式, ARG可设为nosec|mbedtls|tinydtls, 默认tinydtls

例如，将`$(call Build/Configure/Default,--with-endian=big)`改为`$(call Build/Configure/Default,--with-sectype=nosec --with-endian=big)`后，重新`make V=s`，生成的ipk中，加密方式为未加密。

注意，Arduino Yun(ar71xx系列)是大端模式，如果在 Arduino Yun 上安装 SDK，需要配置`--with-endian=big`。
 
