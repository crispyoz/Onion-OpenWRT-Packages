
# Copyright (C) 2016 Onion Corporation
# 
# Author: Lazar Demin  <lazar@onion.io>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=onion-dt-overlay-spi
PKG_VERSION:=1.0
PKG_RELEASE:=1
KERNEL_BUILD_DIR ?= $(BUILD_DIR)/linux-$(BOARD)$(if $(SUBTARGET),_$(SUBTARGET))
LINUX_DIR ?= $(KERNEL_BUILD_DIR)/linux-$(LINUX_VERSION)
DTC=$(LINUX_DIR)/scripts/dtc/dtc

include $(INCLUDE_DIR)/package.mk

# application package
define Package/$(PKG_NAME)
	SECTION:=onion
	CATEGORY:=Onion
	SUBMENU:=Utilities
	TITLE:=Onion DT Overlay for SPI
endef

define Package/$(PKG_NAME)/description
	Onion DT Overlay for SPI
endef

define Build/Prepare
	rm -rf $(PKG_BUILD_DIR)
	mkdir -p $(PKG_BUILD_DIR)
	$(DTC) -b 0 -@ -O dtb src/sw-spi.dts -o $(PKG_BUILD_DIR)/sw-spi.dtbo
endef

define Build/Compile
	true
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/lib/firmware/device-tree/overlays/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/sw-spi.dtbo $(1)/lib/firmware/device-tree/overlays/sw-spi.dtbo
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
