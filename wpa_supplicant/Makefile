include $(TOPDIR)/rules.mk

PKG_NAME:=wpa_supplicant
PKG_VERSION:=2.5
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://hostap.epitest.fi/releases
PKG_MD5SUM:=96ff75c3a514f1f324560a2376f13110

PKG_SOURCE_SUBDIR:=wpa_supplicant

WPA_SUPPLICANT_CONFIG:=$(PKG_BUILD_DIR)/wpa_supplicant/.config

WPA_SUPPLICANT_CONFIG_EDITS =
WPA_SUPPLICANT_CONFIG_ENABLE = \
	CONFIG_IEEE80211AC  \
	CONFIG_IEEE80211N   \
	CONFIG_IEEE80211R   \
	CONFIG_INTERNAL_LIBTOMMATH \
	CONFIG_DEBUG_FILE \
	CONFIG_LIBNL32

WPA_SUPPLICANT_CONFIG_DISABLE += CONFIG_EAP_PWD
WPA_SUPPLICANT_CONFIG_EDITS += 's/\#\(CONFIG_TLS=\).*/\1internal/'

include $(INCLUDE_DIR)/package.mk

define Package/wpa_supplicant
	SECTION:=utils
	CATEGORY:=Utilities
	DEFAULT:=n
	TITLE:=WPA Supplicant
	DEPENDS:=libnl
	URL:=http://hostap.epitest.fi/releases
endef

define Package/wpa_supplicant/description
	WPA Supplicant is a Wi-Fi Protected Access (WPA) client and IEEE 802.1X
	supplicant. It implements WPA key negotiation with a WPA Authenticator
	and Extensible Authentication Protocol (EAP) authentication with an
	Authentication Server. In addition, it controls the roaming and IEEE 802.11
	authentication/association of the wireless LAN driver. This is useful
	for connecting to a password protected wireless access point.
endef

define Build/Compile
	cp $(PKG_BUILD_DIR)/$(PKG_SOURCE_SUBDIR)/defconfig $(WPA_SUPPLICANT_CONFIG)
	sed -i $(patsubst %,-e 's/^#\(%\)/\1/',$(WPA_SUPPLICANT_CONFIG_ENABLE)) \
		$(patsubst %,-e 's/^\(%\)/#\1/',$(WPA_SUPPLICANT_CONFIG_DISABLE)) \
		$(patsubst %,-e %,$(WPA_SUPPLICANT_CONFIG_EDITS)) \
		$(WPA_SUPPLICANT_CONFIG)
	$(call Build/Compile/Default, -C wpa_supplicant all)
endef

define Package/wpa_supplicant/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/$(PKG_SOURCE_SUBDIR)/wpa_supplicant $(1)/usr/sbin
endef

$(eval $(call BuildPackage,wpa_supplicant))
