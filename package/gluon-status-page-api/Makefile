include $(TOPDIR)/rules.mk

PKG_NAME:=gluon-status-page-api
PKG_VERSION:=1
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)
PKG_BUILD_DEPENDS := respondd

include ../gluon.mk


define Package/gluon-status-page-api
  SECTION:=gluon
  CATEGORY:=Gluon
  TITLE:=API for gluon-status-page
  DEPENDS:=+gluon-core +uhttpd +sse-multiplex +gluon-neighbour-info +gluon-respondd +libiwinfo +libjson-c +libnl-tiny +libubus-lua +libbatadv
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./src/* $(PKG_BUILD_DIR)/
endef

define Build/Compile
	$(call Build/Compile/Default)
	$(call GluonSrcDiet,./luasrc,$(PKG_BUILD_DIR)/luadest/)
endef

define Package/gluon-status-page-api/install
	$(INSTALL_DIR) $(1)/lib/gluon/status-page/providers
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/stations $(1)/lib/gluon/status-page/providers/

	$(INSTALL_DIR) $(1)/lib/gluon/respondd
	$(CP) $(PKG_BUILD_DIR)/respondd.so $(1)/lib/gluon/respondd/status-page-api.so

	$(CP) ./files/* $(1)/
	$(CP) $(PKG_BUILD_DIR)/luadest/* $(1)/
endef

$(eval $(call BuildPackage,gluon-status-page-api))
