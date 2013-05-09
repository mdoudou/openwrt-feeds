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
PKG_SOURCE_URL:=http://monkey.org/~marius/
PKG_MD5SUM:=d5de81422b8797afa328f72c694b65bb

include $(INCLUDE_DIR)/package.mk

define Package/nylon
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Web Servers/Proxies
  TITLE:=A SOCKS4/SOCKS5 proxy server
  URL:=http://monkey.org/~marius/nylon/
  DEPENDS:=+libevent
endef

define Package/nylon/conffiles
/etc/nylon.conf
endef

CONFIGURE_ARGS += \
	--with-libevent="$(STAGING_DIR)/usr"

CONFIGURE_VARS += \
	CFLAGS="-D__USE_BSD"

define Package/nylon/install	
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/$(PKG_NAME) $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_DATA) files/$(PKG_NAME).conf.sample $(1)/etc/
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) files/$(PKG_NAME).init $(1)/etc/init.d/$(PKG_NAME)
endef

$(eval $(call BuildPackage,nylon))
