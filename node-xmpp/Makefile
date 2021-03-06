#
# Copyright (C) 2016-2017 LEDE project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NPM_NAME:=xmpp
PKG_NAME:=node-$(PKG_NPM_NAME)
PKG_VERSION:=1.1.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/node-xmpp/node-xmpp.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=b439f45824cfff079c823f6f2c8c67f14237731e
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_MIRROR_HASH:=deccde6e02580d90907c4e4dd20a233290b22fa7c28124bfd60385669b98bc5a

PKG_BUILD_DEPENDS:=node/host node-browserify/host
PKG_USE_MIPS16:=0

PKG_MAINTAINER:=
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=

include $(INCLUDE_DIR)/package.mk

define Package/node-xmpp/default
  DEPENDS:=+node
  SUBMENU:=Node.js
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=XMPP $(1) for JavaScript
  URL:=http://node-xmpp.org/
endef

define Package/node-xmpp
  $(call Package/node-xmpp/default,modules)
endef

define Package/node-xmpp-client
  $(call Package/node-xmpp/default,client)
endef

define Package/node-xmpp-component
  $(call Package/node-xmpp/default,component)
endef

define Package/node-xmpp-server
  $(call Package/node-xmpp/default,server)
endef

define Package/node-xmpp/description
 node-xmpp is a set of JavaScript Node.js, io.js and browser modules to work with XMPP and/or XML
endef

NODEJS_CPU:=$(subst powerpc,ppc,$(subst aarch64,arm64,$(subst x86_64,x64,$(subst i386,ia32,$(ARCH)))))

define Build/Compile/module
	$(MAKE_VARS) \
	$(MAKE_FLAGS) \
	npm_config_arch=$(NODEJS_CPU) \
	npm_config_nodedir=$(STAGING_DIR_HOSTPKG)/ \
	npm_config_cache=$(STAGING_DIR_HOSTPKG)/share/node/npm-cache \
	PREFIX="$(PKG_INSTALL_DIR)/usr/" \
	NODE_PATH="$(PKG_INSTALL_DIR)/usr/lib/node_modules/$(PKG_NAME)/node_modules:$(PKG_INSTALL_DIR)/usr/lib/node_modules/$(PKG_NAME)/node_modules/$(1)/node_modules" \
	npm install --build-from-source --target_arch=$(NODEJS_CPU) -g $(PKG_BUILD_DIR)/packages/$(1)/
endef

define Build/Compile
	$(call Build/Compile/module,node-xmpp)
	$(call Build/Compile/module,node-xmpp-client)
	$(call Build/Compile/module,node-xmpp-component)
	$(call Build/Compile/module,node-xmpp-server)
endef

define Package/node-xmpp/install
	$(INSTALL_DIR) $(1)/usr/lib/node/node-xmpp
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/node_modules/node-xmpp/* $(1)/usr/lib/node/node-xmpp/
endef

define Package/node-xmpp-client/install
	$(INSTALL_DIR) $(1)/usr/lib/node/node-xmpp-client
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/node_modules/node-xmpp-client/* $(1)/usr/lib/node/node-xmpp-client/
endef

define Package/node-xmpp-component/install
	$(INSTALL_DIR) $(1)/usr/lib/node/node-xmpp-component
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/node_modules/node-xmpp-component/* $(1)/usr/lib/node/node-xmpp-component/
endef

define Package/node-xmpp-server/install
	$(INSTALL_DIR) $(1)/usr/lib/node/node-xmpp-server
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/node_modules/node-xmpp-server/* $(1)/usr/lib/node/node-xmpp-server/
endef

$(eval $(call BuildPackage,node-xmpp))
$(eval $(call BuildPackage,node-xmpp-client))
$(eval $(call BuildPackage,node-xmpp-component))
$(eval $(call BuildPackage,node-xmpp-server))
