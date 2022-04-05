#
# Copyright (C) 2019 OpenWrt.org
#
# KFERMercer <KFER.Mercer@gmail.com>
#
# This is free software, licensed under the GNU General Public License v3.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=transfer
PKG_VERSION:=0.4.15
PKG_RELEASE:=$(AUTORELEASE)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/Mikubill/transfer.git
PKG_SOURCE_VERSION:=6da9944560e33d2a79bfe30b38984d7683f4abb6
#PKG_MIRROR_HASH:=2cb9c9e27613cf4126234c969f1928e392108ad4f1580b3eac92339c42a2ab0a

PKG_LICENSE:=MIT License
PKG_LICENSE_FILES:=LICENSE

PKG_CONFIG_DEPENDS:= \
	CONFIG_TRANSFER_COMPRESS_GOPROXY \
	CONFIG_TRANSFER_COMPRESS_UPX

PKG_BUILD_DEPENDS:=golang/host
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

GO_PKG:=github.com/Mikubill/transfer
GO_PKG_LDFLAGS:=-s -w
GO_PKG_LDFLAGS_X:=main.Version=v$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include ../../../feeds/packages/lang/golang/golang-package.mk

define Package/transfer
  TITLE:=Large file transfer tool with multiple file transfer services support
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Web Servers/Proxies
  URL:=https://github.com/Mikubill/transfer
  DEPENDS:=$(GO_ARCH_DEPENDS)
endef

define Package/transfer/description
  Large file transfer tool with multiple file transfer services support
endef

define Package/transfer/config
config TRANSFER_COMPRESS_GOPROXY
	bool "Compiling with GOPROXY proxy"
	default n

config TRANSFER_COMPRESS_UPX
	bool "Compress executable files with UPX"
	depends on !mips64
	default n
endef

ifeq ($(CONFIG_TRANSFER_COMPRESS_GOPROXY),y)
	export GO111MODULE=on
	export GOPROXY=https://goproxy.io
endif

define Build/Compile
	$(call GoPackage/Build/Compile)
ifeq ($(CONFIG_TRANSFER_COMPRESS_UPX),y)
	$(STAGING_DIR_HOST)/bin/upx --lzma --best $(GO_PKG_BUILD_BIN_DIR)/transfer
endif
endef

define Package/transfer/install
	$(call GoPackage/Package/Install/Bin,$(PKG_INSTALL_DIR))
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(GO_PKG_BUILD_BIN_DIR)/transfer $(1)/usr/bin/transfer
endef

$(eval $(call GoBinPackage,transfer))
$(eval $(call BuildPackage,transfer))
