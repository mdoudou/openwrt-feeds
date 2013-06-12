#
# Copyright (C) 2006-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=openvpn_radauth
PKG_VERSION:=1
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git://github.com/melak/$(PKG_NAME).git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=c9564449810736e5d0c9ddd66a433b9ccbc7b98d
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(BUILD_VARIANT)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)/Default
  TITLE:=RADIUS auth script for OpenVPN $(2)
  SECTION:=net
  CATEGORY:=Network
  URL:=http://www.wormhole.hu/~ice/$(PKG_NAME)/
  SUBMENU:=VPN
  DEPENDS:=+openvpn-$(1) $(3)
  VARIANT:=$(1)
  MAINTAINER:=Tamas TEVESZ <ice@extreme.hu>
endef

Package/$(PKG_NAME)-openssl=$(call Package/$(PKG_NAME)/Default,openssl,using OpenSSL,+libopenssl)
Package/$(PKG_NAME)-polarssl=$(call Package/$(PKG_NAME)/Default,polarssl,using PolarSSL,+libpolarssl)
Package/$(PKG_NAME)-nossl=$(call Package/$(PKG_NAME)/Default,nossl,without an SSL library)

Package/$(PKG_NAME)-openssl/config=$(call Package/$(PKG_NAME)/config/Default,openssl)
Package/$(PKG_NAME)-polarssl/config=$(call Package/$(PKG_NAME)/config/Default,polarssl)
Package/$(PKG_NAME)-nossl/config=$(call Package/$(PKG_NAME)/config/Default,nossl)

MAKE_FLAGS+=WITH_SSL_IMPL=$(BUILD_VARIANT)

define Package/$(PKG_NAME)-$(BUILD_VARIANT)/conffiles
/etc/openvpn/radius.conf
endef

define Package/$(PKG_NAME)-$(BUILD_VARIANT)/install	
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_DIR) $(1)/etc/openvpn
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/$(PKG_NAME) $(1)/usr/sbin/
	$(INSTALL_CONF) files/radius.conf.sample $(1)/etc/openvpn/radius.conf
endef

$(eval $(call BuildPackage,$(PKG_NAME)-openssl))
$(eval $(call BuildPackage,$(PKG_NAME)-polarssl))
$(eval $(call BuildPackage,$(PKG_NAME)-nossl))
