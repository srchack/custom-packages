include $(TOPDIR)/rules.mk

PKG_NAME:=fake-hwclock
PKG_VERSION:=0.12
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://git.einval.com/git/fake-hwclock.git
PKG_SOURCE_VERSION:=6652b58ba37566f495cb9b52e71d6858842a2265

PKG_LICENSE:=GPL-2.0

include $(INCLUDE_DIR)/package.mk

define Package/fake-hwclock
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=Save/restore system clock on machines without working RTC hardware
endef

define Package/fake-hwclock/description
	Save/restore system clock on machines without working RTC hardware
endef


define Build/Compile
	true
endef

define Package/fake-hwclock/install
	$(INSTALL_DIR) $(1)/etc/init.d/
	$(INSTALL_BIN) ./files/fake-hwclock.init $(1)/etc/init.d/fake-hwclock
	$(INSTALL_DIR) $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/fake-hwclock $(1)/usr/sbin/
endef

$(eval $(call BuildPackage,fake-hwclock))
