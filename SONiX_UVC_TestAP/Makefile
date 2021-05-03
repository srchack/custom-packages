include $(TOPDIR)/rules.mk

PKG_NAME:=SONiX_UVC_TestAP
PKG_VERSION:=1.0.22
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/Kurokesu/C1_SONIX_Test_AP.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=d3f6c56166b571354969714390cc633c1aa7c3ae

PKG_LICENSE:=GPL-3.0
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk

define Package/SONiX_UVC_TestAP
	SECTION:=utils
	CATEGORY:=Utilities
	DEPENDS:= +libpthread
	TITLE:=SONiX UVC utilitiy
endef

define Package/SONiX_UVC_TestAP/description
	SONiX chipset based USB camera extension unit parameter control toolset
endef

define Package/SONiX_UVC_TestAP/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/SONiX_UVC_TestAP $(1)/usr/bin/
endef

$(eval $(call BuildPackage,SONiX_UVC_TestAP))
