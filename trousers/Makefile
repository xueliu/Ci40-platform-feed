include $(TOPDIR)/rules.mk

PKG_NAME:=trousers
PKG_VERSION:=0.3.13
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/trousers/$(PKG_NAME)/$(PKG_VERSION)
PKG_MD5SUM:=ad508f97b406f6e48cd90e85d78e7ca8
PKG_LICENSE:=CPL-1.0
PKG_LICENSE_FILES:=LICENCE

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Trousers
  URL:=http://trousers.sourceforge.net/
  DEPENDS:=libopenssl kmod-tpm
  USERID:=tss:tss
endef

define Package/$(PKG_NAME)/description
The open-source TCG Software Stack (TSS).

This library enables the use of a Trusted Platform Module that
complies with the TPM specification, version 1.2. It implements the
TSS specification, version 1.2.

endef

define Package/$(PKG_NAME)/conffiles
/etc/tcsd.conf
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/tcsd/tcsd $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/tspi/.libs/libtspi.so* $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_CONF) ./files/tcsd.conf $(1)/etc/
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/tcsd.init $(1)/etc/init.d/tcsd
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_BUILD_DIR)/src/include/trousers $(1)/usr/include/
	$(CP) $(PKG_BUILD_DIR)/src/include/tss $(1)/usr/include/

	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/tspi/.libs/libtspi.so* $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/tddl/libtddl.a $(1)/usr/lib/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
