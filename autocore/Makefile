#
# Copyright (C) 2010-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=autocore
PKG_VERSION:=1
PKG_RELEASE:=29

include $(INCLUDE_DIR)/package.mk

define Package/autocore-arm
  TITLE:=ARM auto core script.
  MAINTAINER:=CN_SZTL
  DEPENDS:=@(TARGET_bcm27xx||TARGET_bcm53xx||TARGET_mvebu||TARGET_ipq40xx||TARGET_ipq806x||TARGET_rockchip) \
    +TARGET_bcm53xx:nvram \
    +TARGET_ipq40xx:lm-sensors \
	+ethtool
  VARIANT:=arm
endef

define Package/autocore-x86
  TITLE:=x86/x64 auto core loadbalance script.
  MAINTAINER:=Lean / CN_SZTL
  DEPENDS:=@TARGET_x86 +bc +lm-sensors +ethtool
  VARIANT:=x86
endef

define Package/autocore-switch
  TITLE:=wireless auto core loadbalance script.
  MAINTAINER:=GaryPang
  DEPENDS:=@swconfig
endef

define Package/autocore-arm/description
  Display more details info about the devices in LuCI.
endef

define Download/armcpuinfo
  URL:=https://raw.githubusercontent.com/immortalwrt/immortalwrt/master/package/lean/autocore/files/arm
  URL_FILE:=cpuinfo
  FILE:=cpuinfo
  HASH:=skip
endef

define Build/Compile
endef

define Package/autocore-arm/install
	$(INSTALL_DIR) $(1)/sbin
	$(INSTALL_BIN) $(DL_DIR)/cpuinfo $(1)/sbin/cpuinfo
	$(INSTALL_DIR) $(1)/www/luci-static/resources/view/status/include
	$(INSTALL_DATA) ./files/arm/* $(1)/www/luci-static/resources/view/status/include/
endef

define Package/autocore-x86/install
	$(INSTALL_DIR) $(1)/sbin
	$(INSTALL_BIN) ./files/x86/cpuinfo $(1)/sbin/cpuinfo
	$(INSTALL_DIR) $(1)/www/luci-static/resources/view/status/include
	$(INSTALL_DATA) ./files/x86/29_eth.js $(1)/www/luci-static/resources/view/status/include/
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/view/admin_status/index/
	$(INSTALL_DATA) ./files/x86/nvme_status.htm $(1)/usr/lib/lua/luci/view/admin_status/index/
endef

define Package/autocore-switch/install
	$(INSTALL_DIR) $(1)/www/luci-static/resources/view/status/include
	$(INSTALL_DATA) ./files/switch/* $(1)/www/luci-static/resources/view/status/include/
endef

$(eval $(call Download,armcpuinfo))
$(eval $(call BuildPackage,autocore-arm))
$(eval $(call BuildPackage,autocore-x86))
$(eval $(call BuildPackage,autocore-switch))
