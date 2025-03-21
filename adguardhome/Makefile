#
# Copyright (C) 2015-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v3.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=adguardhome
PKG_VERSION:=0.108.0-b.64
PKG_RELEASE:=1

PKG_LICENSE:=GPL-3.0-only
PKG_LICENSE_FILES:=LICENSE.txt
PKG_MAINTAINER:=Jack Sun <sunjiazheng321521@gmail.com>

ifeq ($(findstring $(ARCH),x86_64),$(ARCH))
    PKG_ARCH_ADG:=linux_amd64
    PKG_HASH:=
else ifeq ($(findstring $(ARCH),i386),$(ARCH))
    PKG_ARCH_ADG:=linux_386
    PKG_HASH:=
else ifeq ($(findstring $(ARCH),aarch64),$(ARCH))
    PKG_ARCH_ADG:=linux_arm64
    PKG_HASH:=03f44f7dfd64e35aeac44d901329efba89d210c1d9287dccbe01f66554426bef
else ifeq ($(findstring $(ARCH),arm),$(ARCH))
    PKG_ARCH_ADG:=linux_armv7
    PKG_HASH:=
endif

PKG_SOURCE_URL:=https://github.com/AdguardTeam/AdGuardHome/releases/download/v$(PKG_VERSION)/
PKG_SOURCE:=AdGuardHome_$(PKG_ARCH_ADG).tar.gz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/adguardhome
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Network-wide ads and trackers blocking DNS server
  URL:=https://github.com/AdguardTeam/AdGuardHome
endef

define Package/adguardhome/description
  Free and open source, powerful network-wide ads and trackers blocking DNS server.
endef

define Build/Prepare
	gzip -dc $(DL_DIR)/$(PKG_SOURCE) | $(HOST_TAR) -C $(PKG_BUILD_DIR)/ $(TAR_OPTIONS)
endef

define Build/Compile
endef

define Package/adguardhome/install
	$(INSTALL_DIR) $(1)/etc/AdGuardHome
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/AdGuardHome/AdGuardHome $(1)/etc/AdGuardHome
endef

$(eval $(call BuildPackage,adguardhome))