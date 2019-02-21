#
# Copyright (C) 2018 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=open-vm-tools
PKG_VERSION:=10.3.5
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-10430147.tar.gz
PKG_SOURCE_URL:=https://github.com/vmware/open-vm-tools/releases/download/stable-$(PKG_VERSION)
PKG_HASH:=364cd0fdfa5a05e872d08609659e6231ec99788669f7ebba24bfb8c94168daef
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)-10430147
PKG_INSTALL:=1

PKG_FIXUP:=autoreconf
PKG_LICENSE:=LGPL-2.1
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk

define Package/open-vm-tools
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=@TARGET_x86 +glib2 +libpthread +libtirpc
  TITLE:=open-vm-tools
  URL:=https://github.com/vmware/open-vm-tools
  MAINTAINER:=Yuhei OKAWA <tochiro.srchack@gmail.com>
endef

define Package/open-vm-tools-vm-tools/description
	Open Virtual Machine Tools for VMware guest OS
endef


CONFIGURE_ARGS+= \
	--without-icu \
	--disable-multimon \
	--disable-docs \
	--disable-tests \
	--without-gtkmm \
	--without-gtkmm3 \
	--without-xerces \
	--without-pam \
	--disable-grabbitmqproxy \
	--disable-vgauth \
	--disable-deploypkg \
	--without-root-privileges \
	--without-kernel-modules \
	--without-dnet \
	--with-tirpc \
	--without-x \
	--without-gtk2 \
	--without-gtk3 \
	--without-xerces


define Package/open-vm-tools/install
	$(INSTALL_DIR) $(1)/etc/init.d/
	$(INSTALL_BIN) ./files/vmtoolsd.init $(1)/etc/init.d/vmtoolsd

	$(INSTALL_DIR) $(1)/etc/vmware-tools/
	$(INSTALL_DATA) ./files/tools.conf $(1)/etc/vmware-tools/
	$(CP) $(PKG_INSTALL_DIR)/etc/vmware-tools $(1)/etc/

	$(INSTALL_DIR) $(1)/bin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/bin/

	$(INSTALL_DIR) $(1)/sbin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/mount.vmhgfs $(1)/sbin/
	$(INSTALL_BIN) ./files/shutdown $(1)/sbin/

	$(INSTALL_DIR) $(1)/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/lib/

	$(INSTALL_DIR) $(1)/usr/lib/open-vm-tools/plugins/common/
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/open-vm-tools/plugins/common/*.so* $(1)/usr/lib/open-vm-tools/plugins/common/

	$(INSTALL_DIR) $(1)/usr/lib/open-vm-tools/plugins/vmsvc/
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/open-vm-tools/plugins/vmsvc/*.so* $(1)/usr/lib/open-vm-tools/plugins/vmsvc/

	$(INSTALL_DIR) $(1)/etc/hotplug.d/block/
	$(INSTALL_BIN) ./files/vmware-scsi.hotplug $(1)/etc/hotplug.d/block/80-vmware-scsi

	$(INSTALL_DIR) $(1)/usr/share/open-vm-tools/messages/
	$(CP) $(PKG_INSTALL_DIR)/usr/share/open-vm-tools/messages/* $(1)/usr/share/open-vm-tools/messages/
endef

$(eval $(call BuildPackage,open-vm-tools))
