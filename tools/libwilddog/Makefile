#
# Copyright (C) 2006-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libwilddog
PKG_VERSION:=0.8.0
PKG_RELEASE:=5

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://cdn.wilddog.com/c/client/sdk/openwrt/
#PKG_MD5SUM:=509dc27107c21bcd9fbf2f95f5669563
#PKG_MAINTAINER:=Ted Hess <thess@kitschensync.net>

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libwilddog
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=CoAP UDP + DTLS + CBOR
endef

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_INSTALL_DIR:=$(PKG_BUILD_DIR)/ipkg-install



TARGET_CFLAGS += $(FPIC)

define Build/Configure
  $(call Build/Configure/Default,--with-endian=big)
endef

#define Build/Prepare
#	mkdir -p $(PKG_BUILD_DIR)
#endef


define Build/InstallDev
#	mkdir -p $(PKG_INSTALL_DIR)
	$(INSTALL_DIR) $(1)/usr/include/libwilddog
	$(CP) $(PKG_BUILD_DIR)/include/*.h $(1)/usr/include/libwilddog
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/libwilddog.a $(1)/usr/lib/
#	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
#	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/libwilddog.pc $(1)/usr/lib/pkgconfig/
endef

define Package/libwilddog/install
	$(INSTALL_DIR) $(1)/usr/lib
endef

$(eval $(call BuildPackage,libwilddog))
