#
# Copyright (C) 2016-2017 wilddog.com
#
# This is free software, licensed under the MIT License.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libwilddog
PKG_VERSION:=1.0.7
PKG_RELEASE:=5

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://cdn.wilddog.com/sdk/c/$(PKG_VERSION)/

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libwilddog
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=A Library for real-time commuication.
  DEPENDS:=+libpthread
endef

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_INSTALL_DIR:=$(PKG_BUILD_DIR)/ipkg-install



TARGET_CFLAGS += $(FPIC)

define Build/Configure
  $(call Build/Configure/Default,--with-endian=big)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/libwilddog
	$(CP) $(PKG_BUILD_DIR)/include/*.h $(1)/usr/include/libwilddog
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/libwilddog.a $(1)/usr/lib/
endef

define Package/libwilddog/install
	$(INSTALL_DIR) $(1)/usr/lib
endef

$(eval $(call BuildPackage,libwilddog))
