# 
# Copyright (C) 2006-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=siit
PKG_VERSION:=1.1
PKG_RELEASE:=2

include $(INCLUDE_DIR)/package.mk

define KernelPackage/siit
  SUBMENU:=Network Devices
  TITLE:=Stateless IP ICMP Translation Algorithm
  DEPENDS:= @(!(TARGET_ps3||TARGET_pxcab)||BROKEN)
  FILES:=$(PKG_BUILD_DIR)/siit.ko
  AUTOLOAD:=$(call AutoLoad,50,siit)
endef

include $(INCLUDE_DIR)/kernel-defaults.mk

define KernelPackage/siit/description
 Stateless IP ICMP Translation Algorithm
endef

define KernelPackage/siit/install
	$(INSTALL_DIR) $(1)/etc/init.d/
	$(INSTALL_BIN) files/$(PKG_NAME).init $(1)/etc/init.d/$(PKG_NAME)
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	cp src/Makefile src/siit.h src/siit.c $(PKG_BUILD_DIR)/
endef

define Build/Compile
	$(MAKE) $(KERNEL_MAKEOPTS) SUBDIRS="$(PKG_BUILD_DIR)" modules
endef

$(eval $(call KernelPackage,siit))
