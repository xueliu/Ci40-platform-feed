include $(TOPDIR)/rules.mk
PKG_NAME:=proddata
PKG_VERSION:=0.1.1
PKG_RELEASE:=2
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/Creatordev/proddata.git
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_VERSION:=$(PKG_VERSION)
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)

CMAKE_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/proddata
 SECTION:=utils
 CATEGORY:=Utilities
 TITLE:=proddata
 DEPENDS:= +glog
endef

define Package/proddata/description
      Proddata tool.
endef

CMAKE_OPTIONS += -DBUILD_TESTS=OFF -DSTAGING_DIR=$(STAGING_DIR)

define Package/proddata/install
	$(INSTALL_DIR) $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin
	$(INSTALL_DIR) $(1)/usr/lib/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/* $(1)/usr/lib
endef
$(eval $(call BuildPackage,$(PKG_NAME)))
