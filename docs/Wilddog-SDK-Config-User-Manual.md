##WildDog SDK 配置说明

可以在`wilddog-client-openwrt/tools/libwilddog`目录下的Makefile中对sdk进行配置。

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

注意，Arduino Yun(ar71xx系列)是大端模式，如果在Arduino Yun上安装SDK，需要配置`--with-endian=big`。
 