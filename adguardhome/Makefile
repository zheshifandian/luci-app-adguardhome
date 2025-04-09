#
# Copyright (C) 2015-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v3.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=adguardhome
PKG_VERSION:=0.108.0-b.66
PKG_RELEASE:=1

PKG_LICENSE:=GPL-3.0-only
PKG_MAINTAINER:=Jack Sun <sunjiazheng321521@gmail.com>
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)/$(PKG_VERSION)

ifeq ($(findstring $(ARCH),x86_64),$(ARCH))
	PKG_ARCH_ADG:=linux_amd64
	PKG_HASH:=
else ifeq ($(findstring $(ARCH),i386 i686),$(ARCH))
	PKG_ARCH_ADG:=linux_386
	PKG_HASH:=
else ifeq ($(findstring $(ARCH),aarch64 aarch64_be),$(ARCH))
	PKG_ARCH_ADG:=linux_arm64
	PKG_HASH:=skip
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

include $(INCLUDE_DIR)/package.mk

TAR_OPTIONS+= --strip-components 2

define Package/adguardhome
	SECTION:=net
	CATEGORY:=Network
	TITLE:=Network-wide ads and trackers blocking DNS server
	URL:=https://github.com/AdguardTeam/AdGuardHome
	DEPENDS:=+libc +ca-bundle
endef

define Package/adguardhome/description
	Free and open source, powerful network-wide ads and trackers blocking DNS server.
endef

define Package/adguardhome/conffiles
/etc/AdGuardHome/
endef

ADG_FILE:=AdGuardHome_$(PKG_ARCH_ADG)_$(PKG_VERSION).tar.gz
define Download/adguardhome
	URL:=https://github.com/AdguardTeam/AdGuardHome/releases/download/v$(PKG_VERSION)/
	URL_FILE:=AdGuardHome_$(PKG_ARCH_ADG).tar.gz
	FILE:=$(ADG_FILE)
    HASH:=$(PKG_HASH)
endef

define Build/Prepare
	rm -rf $(BUILD_DIR)/$(PKG_NAME)
	mkdir -p $(PKG_BUILD_DIR)
	gzip -dc $(DL_DIR)/$(ADG_FILE) | $(HOST_TAR) -C $(PKG_BUILD_DIR)/ $(TAR_OPTIONS)
endef

define Build/Compile
endef

define Package/adguardhome/install
	$(INSTALL_DIR) $(1)/etc/AdGuardHome
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/AdGuardHome $(1)/etc/AdGuardHome/
endef

$(eval $(call Download,adguardhome))
$(eval $(call BuildPackage,adguardhome))
