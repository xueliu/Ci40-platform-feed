include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=cascoda
PKG_RELEASE:=0.1
PKG_VERSION:=master

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/FlowM2M/ca821x.git
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_VERSION:=$(PKG_VERSION)
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define KernelPackage/cascoda
  SUBMENU:=WPAN 802.15.4 Support
  TITLE:=CASCODA CA821x Driver
  DEPENDS:=@TARGET_pistachio_marduk +kmod-mac802154 +kmod-ieee802154_6lowpan \
           +kmod-nhc_udp +kmod-nhc_fragment +kmod-nhc_dest +kmod-nhc_hop \
           +kmod-nhc_mobility +kmod-nhc_routing +kmod-nhc_ipv6
  FILES:=$(PKG_BUILD_DIR)/Module/ca8210sm.ko
  AUTOLOAD:=$(call AutoLoad,92,ca8210sm)
  KCONFIG:=
endef

define KernelPackage/cascoda/description
 Cascoda ca8210 Driver
endef


EXTRA_CFLAGS+=-I$(PKG_BUILD_DIR)

MAKE_OPTS:= \
        ARCH="$(LINUX_KARCH)" \
        CROSS_COMPILE="$(TARGET_CROSS)" \
        SUBDIRS="$(PKG_BUILD_DIR)" \
        EXTRA_CFLAGS="$(EXTRA_CFLAGS)" \
        $(EXTRA_KCONFIG)


define Build/Compile
	$(MAKE) -C "$(LINUX_DIR)" \
		$(MAKE_OPTS) \
		M=$(PKG_BUILD_DIR)/Module
endef


$(eval $(call KernelPackage,cascoda))

