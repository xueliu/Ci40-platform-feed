include $(TOPDIR)/rules.mk

PKG_NAME:=u-boot
PKG_RELEASE:=1
PKG_VERSION=2015.04

PKG_SOURCE_PROTO:=git
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/CreatorDev/u-boot.git -b master-pistachio
PKG_SOURCE_VERSION:=HEAD

include $(INCLUDE_DIR)/package.mk

define uboot/Default
  TITLE:=
  SOC:=
  DDR_SETTINGS:=
  IMAGE:=
  DEPS:=
endef


define uboot/pistachio_marduk
  TITLE:=U-Boot for Pistachio Marduk
  SOC:=Pistachio
  DEPS:=@TARGET_pistachio
endef

UBOOTS:= \
	pistachio_marduk

define Package/uboot/template
define Package/uboot-$(1)
  SECTION:=boot
  CATEGORY:=Boot Loaders
  DEPENDS:=$(3)
  TITLE:=$(2)
  VARIANT:=$(1)
endef
endef

define Package/uboot/config/template
define Package/uboot-$(1)/config
	source "$(CURDIR)/Config-$(1).in"
endef
endef

define BuildUBootPackage
	$(eval $(uboot/Default))
	$(eval $(uboot/$(1)))
	DEPS:=$(uboot/$(1)/DEPS)
	$(call Package/uboot/template,$(1),$(TITLE),$(DEPS))
	$(call Package/uboot/config/template,$(1))
endef

define Build/Prepare
	$(call Build/Prepare/Default)
endef

define Build/Configure
	$(MAKE) -C $(PKG_BUILD_DIR) $(BUILD_VARIANT)_config
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) CROSS_COMPILE=$(TARGET_CROSS)
endef

define Package/uboot/install/default
	$(CP) \
		$(PKG_BUILD_DIR)/u-boot-pistachio-nor.img \
		$(BIN_DIR)/openwrt-$(BOARD)-$(1)-u-boot.img
endef

define Package/uboot/install/template
define Package/uboot-$(1)/install
	$(call Package/uboot/install/default,$(1),$(if $(IMAGE),$(IMAGE),u-boot.bin))
	$(if $(CONFIG_PACKAGE_UBOOT_SPL), \
		$(CP) $(PKG_BUILD_DIR)/$(call qstrip,$(CONFIG_PACKAGE_UBOOT_SPL_NAME)) $(BIN_DIR)/)
	$(if $(CONFIG_PACKAGE_UBOOT_ENVIMAGE), \
		$(PKG_BUILD_DIR)/tools/mkenvimage -s $(CONFIG_PACKAGE_UBOOT_ENVIMAGE_SIZE) \
		$(if $(CONFIG_PACKAGE_UBOOT_ENVIMAGE_REDUNDANT),-r) \
		-o $(BIN_DIR)/uboot-env.bin $(CONFIG_PACKAGE_UBOOT_ENVIMAGE_SOURCE))
endef
endef


$(foreach u,$(UBOOTS), \
	$(eval $(call BuildUBootPackage,$(u))) \
	$(eval $(call Package/uboot/install/template,$(u))) \
	$(eval $(call BuildPackage,uboot-$(u))) \
)

