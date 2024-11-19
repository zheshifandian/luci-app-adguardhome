#
# Copyright (C) 2015-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v3.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=adguardhome
PKG_VERSION:=0.107.54
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_LICENSE:=GPL-3.0-only
PKG_LICENSE_FILES:=LICENSE.txt
PKG_MAINTAINER:=Dobroslaw Kijowski <dobo90@gmail.com>

include $(INCLUDE_DIR)/package.mk

define Package/adguardhome
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Network-wide ads and trackers blocking DNS server
  URL:=https://github.com/AdguardTeam/AdGuardHome
  DEPENDS:=
endef

define Package/adguardhome/description
  Free and open source, powerful network-wide ads and trackers blocking DNS server.
endef

ifeq ($(ARCH),x86_64)
    PKG_ARCH_ADG := linux_amd64
    PKG_HASH := 00bab072ad10555a431be78723bc54f0da1c4f0c8568d4dc768cdd766edb07e4
else ifeq ($(ARCH),i386)
    PKG_ARCH_ADG := linux_386
    PKG_HASH := 4372d302a874809441e750f5e3f0d913e4a50431fb8c27686790ffc969f0036a
else ifeq ($(ARCH),mipsel)
    PKG_ARCH_ADG := linux_mipsle
    PKG_HASH := afe1ee073c3837d0745b49b2fe5bfed36da209be6778ec1cce573cee933a9b22
else ifeq ($(ARCH),mips)
    PKG_ARCH_ADG := linux_mips64
    PKG_HASH := 7cd2a51678b1bb1deb025a705c740ae2d0d8ed9917bb9d8af85c9c79a2218004
else ifeq ($(ARCH),arm)
    PKG_ARCH_ADG := linux_armv6
    PKG_HASH := 6383bf397bfa7555e9a9532dfae847d60dd09bfa95f4dd8fd347ed9ed5f043c6
else ifeq ($(ARCH),aarch64)
    PKG_ARCH_ADG := linux_arm64
    PKG_HASH := 98111211c49529c7e6db99a63bff8203c0bddcf79f33f04ab4e094b6b962c1fc
endif

ADG_FILE:=AdGuardHome_$(PKG_ARCH_ADG).tar.gz
define Download/adguardhome
	URL:=https://github.com/AdguardTeam/AdGuardHome/releases/download/v$(PKG_VERSION)/
	URL_FILE:=AdGuardHome_$(PKG_ARCH_ADG).tar.gz
	FILE:=$(ADG_FILE)
    HASH:=$(PKG_HASH)
endef

define Build/Prepare
	gzip -dc $(DL_DIR)/$(ADG_FILE) | $(HOST_TAR) -C $(PKG_BUILD_DIR)/ $(TAR_OPTIONS)
endef

define Build/Compile
endef

define Package/adguardhome/install
	$(INSTALL_DIR) $(1)/etc/AdGuardHome
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/AdGuardHome/AdGuardHome $(1)/etc/AdGuardHome
endef

$(eval $(call Download,adguardhome))
$(eval $(call BuildPackage,adguardhome))