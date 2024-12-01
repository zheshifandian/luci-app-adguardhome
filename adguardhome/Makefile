#
# Copyright (C) 2015-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v3.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=adguardhome
PKG_VERSION:=0.107.54
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

PKG_LICENSE:=GPL-3.0-only
PKG_LICENSE_FILES:=LICENSE.txt
PKG_MAINTAINER:=Jack Sun <sunjiazheng321521@gmail.com>

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

ifeq ($(findstring $(ARCH),x86_64 x64 amd64),$(ARCH))
    PKG_ARCH_ADG:=linux_amd64
    PKG_HASH:=
else ifeq ($(findstring $(ARCH),i386 i486 i686 i786 x86),$(ARCH))
    PKG_ARCH_ADG:=linux_386
    PKG_HASH:=
else ifeq ($(ARCH),mips)
    PKG_ARCH_ADG:=linux_mipsle_softfloat
    PKG_HASH:=
else ifeq ($(findstring $(ARCH),mips64 mips64sel),$(ARCH))
    PKG_ARCH_ADG:=linux_mips64sel_softfloat
    PKG_HASH:=
else ifeq ($(ARCH),armv5)
    PKG_ARCH_ADG:=linux_armv5
    PKG_HASH:=
else ifeq ($(ARCH),armv6)
    PKG_ARCH_ADG:=linux_armv6
    PKG_HASH:=
else ifeq ($(ARCH),armv7l)
    PKG_ARCH_ADG:=linux_armv7
    PKG_HASH:=
else ifeq ($(findstring $(ARCH),aarch64 aarch64_be),$(ARCH))
    PKG_ARCH_ADG:=linux_arm64
    PKG_HASH:=
endif

# If you want to check the hash, please complete the "PKG_HASH:=" above (requires sha256), 
# and replace the "HASH:=skip" below with "HASH:=$(PKG_HASH)"

ADG_FILE:=AdGuardHome_$(PKG_ARCH_ADG)_$(PKG_VERSION).tar.gz
define Download/adguardhome
	URL:=https://github.com/AdguardTeam/AdGuardHome/releases/download/v$(PKG_VERSION)/
	URL_FILE:=AdGuardHome_$(PKG_ARCH_ADG).tar.gz
	FILE:=$(ADG_FILE)
    HASH:=skip
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