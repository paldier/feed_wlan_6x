#
# Openwrt Makefile for swpal_6x-uci
#
#

#### Includes ###################################
include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

#### Package Info ############################### 
PKG_NAME:=swpal_6x-uci
PKG_REV:=087caf51ba510e70d0acc85ade0c582207e9c1b9
PKG_VERSION:=1.0.0.1
PKG_RELEASE:=$(PKG_REV)
PKG_BASE_NAME:=$(PKG_NAME)
PKG_SOURCE:=$(PKG_BASE_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=ssh://git@gts-chd.intel.com:29418/sw_wave/swpal.git
PKG_SOURCE_SUBDIR:=$(PKG_BASE_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_SOURCE_PROTO:=git
#PKG_MD5SUM:=40b89c61036add0c2dd1fc10767d3b5f

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_DEFAULT_CUSTOM_SOURCE_DIR:=$(shell pwd)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/package-version-override.mk
## don't remove '-' in the next line - this is part of the Makefile syntax ##
-include $(STAGING_DIR)/mk/ugw-loglevel.mk

define Package/$(PKG_NAME)
  SECTION:=utils
  CATEGORY:=Intel
  SUBMENU:=Static WLAN Platform abstraction layer - SWPAL
  TITLE:=Intel SWPAL
  URL:=http://www.intel.com
  MAINTAINER:=Intel Corporation
  DEPENDS:= +libugwhelper +libcal +csd +servd +libuci +safeclibs
  MENU:=1
endef

define Package/$(PKG_NAME)/description
	Intel SWPAL for WLAN Support
endef

PKG_BUILD_DEPENDS:=libugwhelper libuci

### Menuconfig ##################################
define Package/$(PKG_NAME)/config
$(call Package/$(PKG_NAME)/override_version)
$(call Package/$(PKG_NAME)/override_source_path)
$(call Package/$(PKG_NAME)/config_debug_level)
endef

ifeq ($(CONFIG_USE_MUSL),y)
  TARGET_CFLAGS += -DCONFIG_USE_MUSL
endif
  
TARGET_CFLAGS += -DCONFIG_RPCD

# To ipkg / Rootfs
define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/$(VENDOR_PATH)/usr/lib
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_DIR) $(1)/lib/wifi
	$(INSTALL_DIR) $(1)/lib/netifd
	$(INSTALL_DIR) $(1)/lib/netifd/wireless
	$(INSTALL_DIR) $(1)/lib/config
	$(INSTALL_DIR) $(1)/opt/intel/wave/db
	$(INSTALL_DIR) $(1)/opt/intel/wave/db/11n
	$(INSTALL_DIR) $(1)/opt/intel/wave/db/he
	$(INSTALL_DIR) $(1)/opt/intel/wave/db/he_testbed
	$(INSTALL_DIR) $(1)/opt/intel/wave/db/mbo
	$(INSTALL_DIR) $(1)/opt/intel/wave/db/vht
	$(INSTALL_DIR) $(1)/opt/intel/wave/db/wpa2
	$(INSTALL_DIR) $(1)/opt/intel/wave/db/wpa3
	$(INSTALL_DIR) $(1)/sbin
	$(INSTALL_DIR) $(1)/opt/intel/wave/scripts/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/libspal.so $(1)/$(VENDOR_PATH)/usr/lib
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/scripts/lib/netifd/netifd-wireless.sh $(1)/lib/netifd/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/scripts/lib/netifd/hostapd.sh $(1)/lib/netifd/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/scripts/lib/netifd/debug_infrastructure.sh $(1)/lib/netifd/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/scripts/lib/netifd/debug_post_iw_up.sh $(1)/lib/netifd/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/scripts/lib/netifd/wireless/* $(1)/lib/netifd/wireless/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/scripts/lib/netifd/sigma-ap.sh $(1)/lib/netifd/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/scripts/lib/netifd/sigma-start.sh $(1)/lib/netifd/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/scripts/lib/netifd/sigmaManagerDaemon.sh $(1)/lib/netifd/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/scripts/lib/netifd/terminate_radio_after.sh $(1)/lib/netifd/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/scripts/lib/config/uci.sh $(1)/lib/config/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/scripts/lib/wifi/mac80211.sh $(1)/lib/wifi/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/scripts/lib/wifi/platform_dependent_ugw.sh $(1)/lib/wifi/platform_dependent.sh
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/scripts/sbin/wifi $(1)/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/scripts/etc/wave/scripts/load_dut.sh $(1)/opt/intel/wave/scripts/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/scripts/etc/wave/scripts/flash_file_saver.sh $(1)/opt/intel/wave/scripts/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/scripts/etc/wave/scripts/debug_toolbox.sh $(1)/opt/intel/wave/scripts/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/scripts/etc/wave/scripts/wave_factory_reset.sh $(1)/opt/intel/wave/scripts/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/db/etc/wave/db/wireless* $(1)/opt/intel/wave/db/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/db/etc/wave/db/default* $(1)/opt/intel/wave/db/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/db/etc/wave/db/11n/* $(1)/opt/intel/wave/db/11n
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/db/etc/wave/db/he/* $(1)/opt/intel/wave/db/he
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/db/etc/wave/db/he_testbed/* $(1)/opt/intel/wave/db/he_testbed
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/db/etc/wave/db/mbo/* $(1)/opt/intel/wave/db/mbo
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/db/etc/wave/db/vht/* $(1)/opt/intel/wave/db/vht
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/db/etc/wave/db/wpa2/* $(1)/opt/intel/wave/db/wpa2
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/db/etc/wave/db/wpa3/* $(1)/opt/intel/wave/db/wpa3
	chmod +x $(1)/lib/wifi/mac80211.sh
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_DIR) $(1)/usr/include
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/libspal.so $(1)/usr/lib/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/include/uci_wrapper.h $(1)/usr/include/
endef

define Build/Clean
	if [ -d $(PKG_BUILD_DIR) ]; then $(MAKE) -C $(PKG_BUILD_DIR) clean; \
	$(RM) -r $(PKG_BUILD_DIR)/ipkg-$(BOARD); fi
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
