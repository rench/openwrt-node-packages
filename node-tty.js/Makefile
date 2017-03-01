#
# Copyright (C) 2016-2017 LEDE project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NPM_NAME:=tty.js
PKG_NAME:=node-$(PKG_NPM_NAME)
PKG_VERSION:=0.2.15
PKG_RELEASE:=11

PKG_SOURCE:=$(PKG_NPM_NAME)-$(PKG_VERSION).tgz
PKG_SOURCE_URL:=http://registry.npmjs.org/$(PKG_NPM_NAME)/-/
PKG_MD5SUM:=600f641a8a1ed2edce5599c7e5aee9b6

PKG_BUILD_DEPENDS:=node/host
PKG_USE_MIPS16:=0

PKG_MAINTAINER:=
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk

define Package/node-tty.js
  DEPENDS:=@BROKEN +node
  SUBMENU:=Node.js
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=A terminal for your browser
  URL:=https://www.npmjs.org/package/tty.js
endef

define Package/node-tty.js/description
 A terminal in your browser using node.js and socket.io. Based on Fabrice Bellard's vt100 for jslinux
endef

TAR_OPTIONS+= --strip-components 1
TAR_CMD=$(HOST_TAR) -C $(1) $(TAR_OPTIONS)

CPU:=$(subst powerpc,ppc,$(subst aarch64,arm64,$(subst x86_64,x64,$(subst i386,ia32,$(ARCH)))))

define Build/Compile
	$(MAKE_VARS) \
	$(MAKE_FLAGS) \
	npm_config_arch=$(CPU) \
	npm_config_nodedir=$(STAGING_DIR_HOSTPKG)/ \
	npm_config_cache=$(STAGING_DIR_HOSTPKG)/share/node/npm-cache \
	PREFIX="$(PKG_INSTALL_DIR)/usr/" \
	npm install --build-from-source --target_arch=$(CPU) -g $(PKG_BUILD_DIR)
endef

define Package/node-tty.js/install
	mkdir -p $(1)/usr/lib/node
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/node_modules/* $(1)/usr/lib/node/
	mkdir -p $(1)/usr/bin
	$(LN) ../lib/node/tty.js/bin/tty.js $(1)/usr/bin/tty.js
endef

$(eval $(call BuildPackage,node-tty.js))
