#
# LuCI support for iStoreOS QuickStart (the iStoreOS 首页)
#
# Prebuilt LuCI application from the official iStoreOS release
# 1028-0.17.1-rc20261028 (architecture independent Lua + JS assets).
#
include $(TOPDIR)/rules.mk

PKG_NAME:=luci-app-quickstart
PKG_VERSION:=0.17.1-rc20261028
PKG_RELEASE:=1

PKG_LICENSE:=Apache-2.0
PKG_MAINTAINER:=LinkEase <support@linkease.com>

QUICKSTART_UI_IPK:=luci-app-quickstart_$(PKG_VERSION)-r1_all.ipk

include $(INCLUDE_DIR)/package.mk

define Package/luci-app-quickstart
  SECTION:=luci
  CATEGORY:=LuCI
  SUBMENU:=3. Applications
  TITLE:=LuCI support for iStoreOS QuickStart
  URL:=https://easepi.linkease.com/
  DEPENDS:=+luci-base +luci-lua-runtime +luci-compat +luci-lib-nixio \
	+quickstart +luci-app-store +luci-lib-taskd
endef

define Package/luci-app-quickstart/description
 iStoreOS QuickStart homepage: device overview, network guide, Wi-Fi and
 storage quick controls, plus the /cgi-bin/luci/istore passthrough to the
 QuickStart backend.  Prebuilt from the official iStoreOS alpha release.
endef

define Build/Prepare
	rm -rf $(PKG_BUILD_DIR)
	mkdir -p $(PKG_BUILD_DIR)/_ipk
	$(TAR) -xzf $(CURDIR)/files/$(QUICKSTART_UI_IPK) -C $(PKG_BUILD_DIR)/_ipk
	$(TAR) -xzf $(PKG_BUILD_DIR)/_ipk/data.tar.gz -C $(PKG_BUILD_DIR)
	rm -rf $(PKG_BUILD_DIR)/_ipk
endef

define Build/Compile
endef

define Package/luci-app-quickstart/install
	$(INSTALL_DIR) $(1)/etc $(1)/usr $(1)/www
	$(CP) $(PKG_BUILD_DIR)/etc/. $(1)/etc/
	$(CP) $(PKG_BUILD_DIR)/usr/. $(1)/usr/
	$(CP) $(PKG_BUILD_DIR)/www/. $(1)/www/
endef

$(eval $(call BuildPackage,luci-app-quickstart))
