#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=fcgiwrap
PKG_VERSION:=1.1.0
PKG_RELEASE:=1


PKG_BUILD_DIR := $(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/fcgiwrap/Default
  SECTION:=libs
  CATEGORY:=Libraries
  URL:=https://github.com/gnosek/fcgiwrap
endef

define Package/fcgiwrap
  $(call Package/fcgiwrap/Default)
  MENU:=1
  DEPENDS:=+spawn-fcgi +fcgi
  TITLE:=fcgiwrap
endef


define Package/fcgiwrap/description
 fcgiwrap
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./src/* $(PKG_BUILD_DIR)/
endef

define Build/Configure
        $(call Build/Configure/Default)
endef

define Build/Compile
$(call Build/Compile/Default)
endef

define Package/fcgiwrap/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/fcgiwrap $(1)/usr/bin/
endef


$(eval $(call BuildPackage,fcgiwrap))
