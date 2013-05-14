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

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://www.wormhole.hu/~ice/$(PKG_NAME)
PKG_MD5SUM:=c9cecdcb30a93183a80c6d383416050d

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(BUILD_VARIANT)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/openvpn_radauth/Default
  TITLE:=RADIUS auth script for OpenVPN using $(2)
  SECTION:=net
  CATEGORY:=Network
  URL:=http://www.wormhole.hu/~ice/openvpn_radauth/
  SUBMENU:=VPN
  DEPENDS:=+openvpn-$(1) $(3)
  VARIANT:=$(1)
  MAINTAINER:=Tamas TEVESZ <ice@extreme.hu>
endef

Package/openvpn_radauth-openssl=$(call Package/openvpn_radauth/Default,openssl,OpenSSL,+libopenssl)
Package/openvpn_radauth-polarssl=$(call Package/openvpn_radauth/Default,polarssl,PolarSSL,+libpolarssl)

Package/openvpn_radauth-openssl/config=$(call Package/openvpn_radauth/config/Default,openssl)
Package/openvpn_radauth-polarssl/config=$(call Package/openvpn_radauth/config/Default,polarssl)

MAKE_FLAGS+=WITH_SSL_IMPL=$(BUILD_VARIANT)

define Package/openvpn_radauth-$(BUILD_VARIANT)/conffiles
/etc/openvpn/radius.conf
endef

define Package/openvpn_radauth-$(BUILD_VARIANT)/install	
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_DIR) $(1)/etc/openvpn
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/$(PKG_NAME) $(1)/usr/sbin/
	$(INSTALL_CONF) files/radius.conf.sample $(1)/etc/openvpn/radius.conf
endef

$(eval $(call BuildPackage,openvpn_radauth-openssl))
$(eval $(call BuildPackage,openvpn_radauth-polarssl))
