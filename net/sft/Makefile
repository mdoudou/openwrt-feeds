#
# Copyright (C) 2006-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=sft
PKG_VERSION:=0.4.14
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://nbenoit.tuxfamily.org/projects/$(PKG_NAME)/
PKG_MD5SUM:=01ba22dd4af970c8e9e9732e14129610

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=File Transfer
  TITLE:=A simple file transfer tool
  URL:=http://nbenoit.tuxfamily.org/index.php?page=SFT
  MAINTAINER:=Tamas TEVESZ <ice@extreme.hu>
endef

define Package/$(PKG_NAME)/install	
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/$(PKG_NAME) $(1)/usr/bin/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
