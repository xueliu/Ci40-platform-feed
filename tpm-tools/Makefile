include $(TOPDIR)/rules.mk

PKG_NAME:=tpm-tools
PKG_VERSION:=1.3.8
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/trousers/$(PKG_NAME)/$(PKG_VERSION)
PKG_MD5SUM:=85a978c4e03fefd4b73cbeadde7c4d0b
PKG_FIXUP:=autoreconf
PKG_LICENSE:=CPL-1.0
PKG_LICENSE_FILES:=LICENCE

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=TPM tools
  URL:=http://trousers.sourceforge.net/
  DEPENDS:=+trousers libopenssl
endef

define Package/$(PKG_NAME)/description
  Tools to manage and diagnose a TPM

endef

define Package/$(PKG_NAME)/install

	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lib/.libs/libtpm_unseal.so* $(1)/usr/lib

	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/cmds/.libs/tpm_sealdata $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/cmds/.libs/tpm_unsealdata $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/tpm_mgmt/tpm_changeownerauth $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/tpm_mgmt/tpm_clear $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/tpm_mgmt/tpm_createek $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/tpm_mgmt/tpm_getpubek $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/tpm_mgmt/tpm_restrictpubek $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/tpm_mgmt/tpm_setactive $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/tpm_mgmt/tpm_setenable $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/tpm_mgmt/tpm_setclearable $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/tpm_mgmt/tpm_setownable $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/tpm_mgmt/tpm_setpresence $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/tpm_mgmt/tpm_takeownership $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/tpm_mgmt/tpm_version $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/tpm_mgmt/tpm_selftest $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/tpm_mgmt/tpm_nvdefine $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/tpm_mgmt/tpm_nvinfo $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/tpm_mgmt/tpm_nvread $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/tpm_mgmt/tpm_nvrelease $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/tpm_mgmt/tpm_nvwrite $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/tpm_mgmt/tpm_resetdalock $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/tpm_mgmt/tpm_restrictsrk $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/tpm_mgmt/tpm_revokeek $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/tpm_mgmt/tpm_setoperatorauth $(1)/usr/bin

endef

$(eval $(call BuildPackage,$(PKG_NAME)))
