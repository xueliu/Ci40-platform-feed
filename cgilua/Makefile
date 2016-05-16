include $(TOPDIR)/rules.mk

PKG_NAME:=cgilua
PKG_VERSION:=v5.1.4
PKG_RELEASE:=1
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/keplerproject/cgilua.git

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_VERSION:=$(PKG_VERSION)
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/cgilua
	SECTION:=utils
	CATEGORY:=Utilities
	DEFAULT:=n
	DEPENDS:= +lua +lua-coxpcall
	TITLE:=CGILua library
	URL:=http://github.com/downloads/keplerproject/cgilua/
endef

define Package/cgilua/description
	CGILua allows the separation of logic and data handling from the
	generation of pages, making it easy to develop web applications with
	Lua. CGILua can be used with a variety of Web servers and, for each
	server, with different launchers. A launcher is responsible for the
	interaction of CGILua and the Web server, for example using ISAPI on
	IIS or mod_lua on Apache.
endef

define Build/Compile
	$(call Build/Compile/Default, install LUA_DIR=$(PKG_BUILD_DIR)/lua)
endef

define Package/cgilua/install
	$(INSTALL_DIR) $(1)/usr/lib/lua
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lua/cgilua.lua $(1)/usr/lib/lua
	$(INSTALL_DIR) $(1)/usr/lib/lua/cgilua
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lua/cgilua/* $(1)/usr/lib/lua/cgilua
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/launchers/cgilua.cgi $(1)/usr/bin
endef


$(eval $(call BuildPackage,cgilua))
