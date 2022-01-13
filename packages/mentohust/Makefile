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


PKG_FIXUP:=autoreconf

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/mentohust
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libpcap
  TITLE:=A Ruijie Client Daemon
  URL:=mentohust-0.3.1.tar.gz
  SUBMENU:=Ruijie
endef

define Package/mentohust/description
A Ruijie Client Daemon,
Most usually used in China collages.
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	tar xf ../../dl/mentohust-0.3.1.tar.gz 
	mv mentohust-0.3.1/* $(PKG_BUILD_DIR)/
	cp -r etc $(PKG_BUILD_DIR)/
	rm -rf mentohust-0.3.1
	$(SED) 's/dhclient/udhcpc -i/g' $(PKG_BUILD_DIR)/src/myconfig.c
endef


define Package/mentohust/conffiles
/etc/mentohust.conf
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
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/etc/mentohust.conf $(1)/etc/mentohust.conf

endef

$(eval $(call BuildPackage,$(PKG_NAME)))
