#
# Copyright (C) 2006-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=nylon
PKG_VERSION:=1.21
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://monkey.org/~marius/$(PKG_NAME)
PKG_MD5SUM:=d5de81422b8797afa328f72c694b65bb

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Web Servers/Proxies
  TITLE:=A SOCKS4(a)/SOCKS5 proxy server
  URL:=http://monkey.org/~marius/$(PKG_NAME)/
  DEPENDS:=+libevent2
  MAINTAINER:=Tamas TEVESZ <ice@extreme.hu>
endef

define Package/$(PKG_NAME)/conffiles
/etc/$(PKG_NAME).conf
endef

CONFIGURE_ARGS += \
	--with-libevent="$(STAGING_DIR)/usr"

CONFIGURE_VARS += \
	CFLAGS="-D_BSD_SOURCE"

define Package/$(PKG_NAME)/install	
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/$(PKG_NAME) $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_DATA) files/$(PKG_NAME).conf.sample $(1)/etc/$(PKG_NAME).conf
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) files/$(PKG_NAME).init $(1)/etc/init.d/$(PKG_NAME)
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
