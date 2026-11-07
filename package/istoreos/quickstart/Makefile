#
# iStoreOS QuickStart homepage backend (prebuilt binary)
#
# The binary is taken unchanged from the official iStoreOS release
#   1028-0.17.1-rc20261028  (https://fw.koolcenter.com/iStoreOS/alpha/quickstart/)
# arm64 build.  It is a statically linked aarch64 musl Go binary, so it runs on
# the qualcommax / IPQ6010 target without recompiling.  The package manager
# (opkg or apk) is detected at runtime by the binary itself.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=quickstart
PKG_VERSION:=0.17.1-rc20261028
PKG_RELEASE:=1

PKG_LICENSE:=Apache-2.0
PKG_MAINTAINER:=LinkEase <support@linkease.com>

QUICKSTART_IPK:=quickstart_$(PKG_VERSION)-r1_aarch64_generic.ipk

include $(INCLUDE_DIR)/package.mk

define Package/quickstart
  SECTION:=net
  CATEGORY:=Network
  TITLE:=iStoreOS QuickStart homepage backend
  URL:=https://easepi.linkease.com/
  DEPENDS:=+bash +block-mount +e2fsprogs +lsblk +ip-full +parted +mdadm \
	+smartmontools +shadow-utils +mount-utils +ca-bundle
endef

define Package/quickstart/description
 iStoreOS QuickStart (iStoreOS 首页) backend service.  Provides the device
 dashboard, network guide and storage/NAS helpers used by luci-app-quickstart.
 Prebuilt aarch64 binary from the official iStoreOS alpha release.
endef

define Package/quickstart/conffiles
/etc/config/quickstart
endef

define Build/Prepare
	rm -rf $(PKG_BUILD_DIR)
	mkdir -p $(PKG_BUILD_DIR)/_ipk
	$(TAR) -xzf $(CURDIR)/files/$(QUICKSTART_IPK) -C $(PKG_BUILD_DIR)/_ipk
	$(TAR) -xzf $(PKG_BUILD_DIR)/_ipk/data.tar.gz -C $(PKG_BUILD_DIR)
	rm -rf $(PKG_BUILD_DIR)/_ipk
endef

define Build/Compile
endef

define Package/quickstart/install
	$(INSTALL_DIR) $(1)/etc $(1)/lib $(1)/usr
	$(CP) $(PKG_BUILD_DIR)/etc/. $(1)/etc/
	$(CP) $(PKG_BUILD_DIR)/lib/. $(1)/lib/
	$(CP) $(PKG_BUILD_DIR)/usr/. $(1)/usr/
	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_BIN) ./files/90-quickstart-enable $(1)/etc/uci-defaults/90-quickstart-enable
endef

$(eval $(call BuildPackage,quickstart))
