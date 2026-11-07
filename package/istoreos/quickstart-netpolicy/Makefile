#
# iStoreOS quickstart-netpolicy (prebuilt eBPF network policy engine)
#
# Unchanged binary from the official iStoreOS release 1028-0.17.1-rc20261028.
# Provides per-device rate limits / network policy for the QuickStart homepage.
# Statically linked aarch64 musl binary.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=quickstart-netpolicy
PKG_VERSION:=0.2.0
PKG_RELEASE:=1

PKG_LICENSE:=Apache-2.0
PKG_MAINTAINER:=LinkEase <support@linkease.com>

NETPOLICY_IPK:=quickstart-netpolicy_0.2.0-test20260928-r3_aarch64_generic.ipk

include $(INCLUDE_DIR)/package.mk

define Package/quickstart-netpolicy
  SECTION:=net
  CATEGORY:=Network
  TITLE:=QuickStart eBPF network policy engine
  URL:=https://github.com/istoreos/quickstart-netpolicy
  DEPENDS:=+ca-bundle
endef

define Package/quickstart-netpolicy/description
 Independent eBPF network-policy engine used by the QuickStart homepage for
 device rate limits and quotas.  Prebuilt aarch64 binary from iStoreOS.
endef

define Package/quickstart-netpolicy/conffiles
/etc/config/quickstart-netpolicy
endef

define Build/Prepare
	rm -rf $(PKG_BUILD_DIR)
	mkdir -p $(PKG_BUILD_DIR)/_ipk
	$(TAR) -xzf $(CURDIR)/files/$(NETPOLICY_IPK) -C $(PKG_BUILD_DIR)/_ipk
	$(TAR) -xzf $(PKG_BUILD_DIR)/_ipk/data.tar.gz -C $(PKG_BUILD_DIR)
	rm -rf $(PKG_BUILD_DIR)/_ipk
endef

define Build/Compile
endef

define Package/quickstart-netpolicy/install
	$(INSTALL_DIR) $(1)/etc $(1)/usr
	$(CP) $(PKG_BUILD_DIR)/etc/. $(1)/etc/
	$(CP) $(PKG_BUILD_DIR)/usr/. $(1)/usr/
endef

$(eval $(call BuildPackage,quickstart-netpolicy))
