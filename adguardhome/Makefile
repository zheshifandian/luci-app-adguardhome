#
# Copyright (C) 2015-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v3.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=adguardhome
PKG_VERSION:=0.108.0-b.62
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

ifeq ($(findstring $(ARCH),x86_64),$(ARCH))
    PKG_ARCH_ADG:=linux_amd64
    PKG_HASH:=
else ifeq ($(findstring $(ARCH),i386),$(ARCH))
    PKG_ARCH_ADG:=linux_386
    PKG_HASH:=
else ifeq ($(findstring $(ARCH),aarch64),$(ARCH))
    PKG_ARCH_ADG:=linux_arm64
    PKG_HASH:=
else ifeq ($(findstring $(ARCH),arm),$(ARCH))
    PKG_ARCH_ADG:=linux_armv7
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