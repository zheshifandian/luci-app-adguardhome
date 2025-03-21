#
# Copyright (C) 2015-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v3.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=adguardhome
PKG_VERSION:=0.108.0-b.65
PKG_RELEASE:=1

PKG_LICENSE:=GPL-3.0-only
PKG_LICENSE_FILES:=LICENSE.txt
PKG_MAINTAINER:=Jack Sun <sunjiazheng321521@gmail.com>

ifeq ($(findstring $(ARCH),x86_64),$(ARCH))
	PKG_ARCH_ADG:=linux_amd64
	PKG_HASH:=
else ifeq ($(findstring $(ARCH),i386 i686),$(ARCH))
	PKG_ARCH_ADG:=linux_386
	PKG_HASH:=
else ifeq ($(findstring $(ARCH),aarch64 aarch64_be),$(ARCH))
	PKG_ARCH_ADG:=linux_arm64
	PKG_HASH:=891d9eb1db6b9a95e9dd6e6ff03f8fc0979c6ba841cfac5cd736bf7bdc0854a2
else ifeq ($(findstring $(ARCH),arm armeb),$(ARCH))
	PKG_ARCH_ADG:=linux_armv7
	PKG_HASH:=
else ifeq ($(findstring $(ARCH),mips),$(ARCH))
	PKG_ARCH_ADG:=linux_mips_softfloat
	PKG_HASH:=
else ifeq ($(findstring $(ARCH),mipsel),$(ARCH))
	PKG_ARCH_ADG:=linux_mipsle_softfloat
	PKG_HASH:=
else ifeq ($(findstring $(ARCH),mips64),$(ARCH))
	PKG_ARCH_ADG:=linux_mips64_softfloat
	PKG_HASH:=
else ifeq ($(findstring $(ARCH),powerpc64),$(ARCH))
	PKG_ARCH_ADG:=linux_ppc64le_softfloat
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
	$(TAR) -C $(PKG_BUILD_DIR) -xf $(DL_DIR)/$(PKG_SOURCE) --strip-components 2
endef

define Build/Compile
endef

define Package/adguardhome/install
	$(INSTALL_DIR) $(1)/etc/AdGuardHome
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/AdGuardHome $(1)/etc/AdGuardHome/
endef

$(eval $(call BuildPackage,adguardhome))
