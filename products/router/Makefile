
# (C) 2013-2014 CarrierWrt.org
# (C) 2015 ConnectedTEK, a division of OptionWell LLC

#
# Product profile: router (Consumer Wi-Fi Router)
#

define Product/router

	CONFIG += \
		CONFIG_PACKAGE_luci=y \
		CONFIG_PACKAGE_anyfi-mac=y
			
endef

define Customization/default

	CONFIG += \
		CONFIG_PACKAGE_luci-theme-bootstrap=y \
		CONFIG_PACKAGE_luci-branding=y \
		CONFIG_PACKAGE_easycwmp=y
	
	TESTED := \
		ar71xx/openwrt-ar71xx-generic-tl-wr841n-v8-squashfs-factory.bin \
		ar71xx/openwrt-ar71xx-generic-tl-wr841n-v8-squashfs-sysupgrade.bin

	TR69_MIGR_DIR := $(OPENWRT_DIR)/files/etc/uci-migrations/1.1.3-6

endef

define Customization/default/prebuild
	mkdir -p $(TR69_MIGR_DIR)
	cp common/uci-migrations/tr69/set-fixed-acs.sh $(TR69_MIGR_DIR)/01-tr69-set-fixed-acs.sh
	cp common/uci-migrations/tr69/open-firewall.sh $(TR69_MIGR_DIR)/02-tr69-open-firewall.sh
	cp common/uci-migrations/tr69/fixup-wan-if.sh  $(TR69_MIGR_DIR)/03-tr69-fixup-wan-if.sh
endef

define Customization/debug
	$(call Customization/default)

	CONFIG += \
		CONFIG_BUSYBOX_CONFIG_FEATURE_INIT_COREDUMPS=y \
		CONFIG_PACKAGE_ATH_DEBUG=y \
		CONFIG_PACKAGE_hostapd-utils=y

	LOG_MIGR_DIR := $(OPENWRT_DIR)/files/etc/uci-migrations/1.1.3-8
endef

define Customization/debug/prebuild
	touch $(OPENWRT_DIR)/files/.init_enable_core
	rm $(LOG_MIGR_DIR)/01-log-set-level-info.sh
	cp common/uci-migrations/log/set-level-debug.sh $(LOG_MIGR_DIR)/01-log-set-level-debug.sh
endef

