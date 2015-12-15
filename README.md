
####wilddog-client-openwrt说明：

`wilddog-client-openwrt`SDK提供了一整套访问和操作野狗云端数据的`API`，用户只需要在`openwrt`上安装`SDK`，即可在应用中调用野狗提供的[API](https://z.wilddog.com/device/quickstart)访问野狗云端的数据.

#####1. 下载

从git下载到文件夹

	git clone https://github.com/WildDogTeam/wilddog-client-openwrt.git

#####2. 部署到openwrt项目中

将`wilddog-client-openwrt/tools/libwilddog`文件夹拷贝到`openwrt`项目中的`package/libs/`目录下.

	cp -rf wilddog-client-openwrt/tools/libwilddog  <your openwrt path>/package/libs/

#####3. 在openwrt项目下制作ipk并安装

1. 在openwrt项目的根目录下运行`make menuconfig`；

2. 在`Libraries`目录下，选中`libwilddog`，并设置为module（如果设置为built-in，则可忽略3、4两步,但需要将整个openwrt固件刷到设备中);

		{M} libwilddog........................................ CoAP UDP + DTLS + CBOR

3. 运行make编译openwrt；

4. 编译成功后，在`bin`目录下能找到`libwilddog_x.x.x-x_xxxx.ipk`；

5. 将这个ipk上传到openwrt中，并opkg安装

		opkg install libwilddog_x.x.x-x_xxxx.ipk


#####4.范例使用


1. 将`wilddog-client-openwrt/examples/demo`文件夹（以及其中的`Makefile`文件）拷贝到`openwrt`项目中的`package/utils/`目录下.

	 cp -rf wilddog-client-openwrt/examples/demo  <your openwrt path>/package/utils/

2. 配置，生成`demo.ipk`，执行`make menuconfig`，在`Utilities`选中`demo`，并设置为module;
	
		<M> demo............................ demo -- demo show how to use libwilddog 

3. 编译：

	make V=s

4. 将编译出来的`bin`目录下的`demo_x_xxxx.ipk`上传到`openwrt`中，并`opkg`安装;

	opkg install demo_x_xxxx.ipk

5. 使用demo获取数据:

	demo getValue -l coap://yourappid.wilddogio.com/YourPath 

`yourappid`为在野狗上申请的应用名称.

6. 该demo展示了如何获取、更新、删除野狗云端数据，具体使用请阅读源码.
	 		
