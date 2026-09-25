include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=rtl8188eu
PKG_VERSION:=5.2.2.4
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/Benetti-Engineering/rtl8188eu.git
PKG_SOURCE_DATE:=2024-01-01
PKG_SOURCE_VERSION:=cca7c28087db740d7d745e81e4096c9eb9084f9a
PKG_MIRROR_HASH:=skip

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define KernelPackage/rtl8188eu
  SUBMENU:=Wireless Drivers
  TITLE:=Realtek RTL8188EU (out-of-tree)
  DEPENDS:=@USB_SUPPORT +kmod-usb-core +kmod-cfg80211
  FILES:=$(PKG_BUILD_DIR)/8188eu.ko
  AUTOLOAD:=$(call AutoProbe,8188eu)
endef

define KernelPackage/rtl8188eu/description
  Realtek RTL8188EU USB Wi-Fi driver, built out-of-tree from the
  Benetti-Engineering fork (branch v5.2.2.4, commit cca7c28).
endef

define Build/Compile
	$(MAKE) -C "$(LINUX_DIR)" \
		$(KERNEL_MAKE_FLAGS) \
		M="$(PKG_BUILD_DIR)" \
		CONFIG_RTL8188EU=m \
		modules
endef

$(eval $(call KernelPackage,rtl8188eu))