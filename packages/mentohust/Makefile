#
# Copyright (C) 2014-2015 KyleRicardo
#
# This is free software, licensed under the GNU General Public License v3.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mentohust
PKG_VERSION:=0.3.1
PKG_RELEASE:=1
PKG_SOURCE:=mentohust-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://raw.githubusercontent.com/dsjlkw/mentohust/master/dl
PKG_HASH:=c7033ba8d8e75294924ed03f4b7b0c45

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/mentohust
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libpcap
  TITLE:=A Ruijie Client Daemon
  URL:=https://raw.githubusercontent.com/dsjlkw/mentohust/master/dl
endef

CONFIGURE_ARGS += \
	--disable-encodepass \
	--disable-notify \

define Package/mentohust/description
A Ruijie Client Daemon,
Most usually used in China collages.
endef

define Package/mentohust/conffiles
/etc/config/mentohust.conf
endef

define Build/Compile
	#$(Build/Compile/$(PKG_NAME))
	$(MAKE) -C $(PKG_BUILD_DIR)/ \
		$(TARGET_CONFIGURE_OPTS) \
		CFLAGS="$(TARGET_CFLAGS)" \
		CPPFLAGS="$(TARGET_CPPFLAGS)"  \
		LDFLAGS="$(TARGET_LDFLAGS) -ldl"
endef

define Package/mentohust/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/mentohust $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/etc/config
	$(CP) ./files/etc/* $(1)/etc/config/

endef

$(eval $(call BuildPackage,$(PKG_NAME)))
