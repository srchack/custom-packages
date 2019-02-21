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

PKG_FIXUP:=autoreconf
PKG_LICENSE:=LGPL-2.1

include $(INCLUDE_DIR)/package.mk

define Package/open-vm-tools
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=@TARGET_x86 +glib2 +libpthread +libtirpc
  TITLE:=open-vm-tools
  URL:=https://github.com/vmware/open-vm-tools
  MAINTAINER:=YuheiOKAWA <tochiro.srchack@gmail.com>
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
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/scripts/poweroff-vm-default $(1)/etc/vmware-tools/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/scripts/poweron-vm-default $(1)/etc/vmware-tools/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/scripts/resume-vm-default $(1)/etc/vmware-tools/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/scripts/suspend-vm-default $(1)/etc/vmware-tools/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/scripts/common/statechange.subr $(1)/etc/vmware-tools/

	$(INSTALL_DIR) $(1)/etc/vmware-tools/scripts/vmware/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/scripts/linux/network $(1)/etc/vmware-tools/scripts/vmware/

	$(INSTALL_DIR) $(1)/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/checkvm/.libs/vmware-checkvm $(1)/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/namespacetool/.libs/vmware-namespace-cmd $(1)/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/xferlogs/.libs/vmware-xferlogs $(1)/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/hgfsclient/.libs/vmware-hgfsclient $(1)/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/services/vmtoolsd/.libs/vmtoolsd $(1)/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/rpctool/vmware-rpctool $(1)/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/toolbox/.libs/vmware-toolbox-cmd $(1)/bin/

	$(INSTALL_DIR) $(1)/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/hgfsmounter/mount.vmhgfs $(1)/sbin/
	$(INSTALL_BIN) ./files/shutdown $(1)/sbin/

	$(INSTALL_DIR) $(1)/lib/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/libhgfs/.libs/libhgfs.so.0.0.0 $(1)/lib/
	$(LN) libhgfs.so.0.0.0 $(1)/lib/libhgfs.so.0
	$(LN) libhgfs.so.0.0.0 $(1)/lib/libhgfs.so
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/libguestlib/.libs/libguestlib.so.0.0.0 $(1)/lib/
	$(LN) libguestlib.so.0.0.0 $(1)/lib/libguestlib.so.0
	$(LN) libguestlib.so.0.0.0 $(1)/lib/libguestlib.so
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/libvmtools/.libs/libvmtools.so.0.0.0 $(1)/lib/
	$(LN) libvmtools.so.0.0.0 $(1)/lib/libvmtools.so.0
	$(LN) libvmtools.so.0.0.0 $(1)/lib/libvmtools.so

	$(INSTALL_DIR) $(1)/usr/lib/open-vm-tools/plugins/common/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/services/plugins/vix/.libs/libvix.so $(1)/usr/lib/open-vm-tools/plugins/common/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/services/plugins/hgfsServer/.libs/libhgfsServer.so $(1)/usr/lib/open-vm-tools/plugins/common/

	$(INSTALL_DIR) $(1)/usr/lib/open-vm-tools/plugins/vmsvc/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/services/plugins/resolutionKMS/.libs/libresolutionKMS.so $(1)/usr/lib/open-vm-tools/plugins/vmsvc/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/services/plugins/powerOps/.libs/libpowerOps.so $(1)/usr/lib/open-vm-tools/plugins/vmsvc/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/services/plugins/timeSync/.libs/libtimeSync.so $(1)/usr/lib/open-vm-tools/plugins/vmsvc/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/services/plugins/guestInfo/.libs/libguestInfo.so $(1)/usr/lib/open-vm-tools/plugins/vmsvc/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/services/plugins/vmbackup/.libs/libvmbackup.so $(1)/usr/lib/open-vm-tools/plugins/vmsvc/

	$(INSTALL_DIR) $(1)/lib/udev/rules.d/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/udev/99-vmware-scsi-udev.rules $(1)/lib/udev/rules.d/

	$(INSTALL_DIR) $(1)/usr/share/open-vm-tools/messages/ko/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/services/vmtoolsd/l10n/ko.vmsg $(1)/usr/share/open-vm-tools/messages/ko/vmtoolsd.vmsg
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/toolbox/l10n/ko.vmsg $(1)/usr/share/open-vm-tools/messages/ko/toolboxcmd.vmsg
	$(INSTALL_DIR) $(1)/usr/share/open-vm-tools/messages/de/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/services/vmtoolsd/l10n/de.vmsg $(1)/usr/share/open-vm-tools/messages/de/vmtoolsd.vmsg
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/toolbox/l10n/de.vmsg $(1)/usr/share/open-vm-tools/messages/de/toolboxcmd.vmsg
	$(INSTALL_DIR) $(1)/usr/share/open-vm-tools/messages/ja/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/services/vmtoolsd/l10n/ja.vmsg $(1)/usr/share/open-vm-tools/messages/ja/vmtoolsd.vmsg
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/toolbox/l10n/ja.vmsg $(1)/usr/share/open-vm-tools/messages/ja/toolboxcmd.vmsg
	$(INSTALL_DIR) $(1)/usr/share/open-vm-tools/messages/zh_CN/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/toolbox/l10n/zh_CN.vmsg $(1)/usr/share/open-vm-tools/messages/zh_CN/toolboxcmd.vmsg
endef

$(eval $(call BuildPackage,open-vm-tools))
