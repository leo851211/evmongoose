
include $(TOPDIR)/rules.mk

PKG_NAME:=evmongoose
PKG_VERSION:=2017-5-27
PKG_RELEASE:=$(PKG_SOURCE_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/zhaojh329/evmongoose.git
PKG_SOURCE_VERSION:=4724d4d5cf8a5896a2e409401974b60b84760771
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz

PKG_CONFIG_DEPENDS:= CONFIG_EVMONGOOSE_SSL_NONE CONFIG_EVMONGOOSE_SSL_OPENSSL CONFIG_EVMONGOOSE_SSL_MBEDTLS

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/evmongoose
  SECTION:=libs
  CATEGORY:=Libraries
  SUBMENU:=Networking
  TITLE:=Mongoose Embedded Web Server Library(based on libev)
  URL:=https://github.com/zhaojh329/evmongoose
  DEPENDS:=+libev +EVMONGOOSE_SSL_OPENSSL:libopenssl +EVMONGOOSE_SSL_MBEDTLS:libmbedtls
endef

define Package/evmongoose/description
	Evmongoose is an api friendly and scalable 
	HTTP server library based on mongoose and libev.
endef

define Package/evmongoose/config
menu "Configuration"
	depends on PACKAGE_evmongoose

	choice
		prompt "SSl"
		default EVMONGOOSE_SSL_NONE
		
		config EVMONGOOSE_SSL_NONE
			bool "none"
			
		config EVMONGOOSE_SSL_OPENSSL
			bool "openssl"
			
		config MONGOOSE_SSL_MBEDTLS
			bool "mbedtls"
		
	endchoice
endmenu
endef

CMAKE_OPTIONS = -DHTTPS_SUPPORT=OFF

ifeq ($(CONFIG_EVMONGOOSE_SSL_OPENSSL),y)
  CMAKE_OPTIONS = -DHTTPS_SUPPORT=ON
endif

ifeq ($(CONFIG_EVMONGOOSE_SSL_MBEDTLS),y)
  CMAKE_OPTIONS = -DHTTPS_SUPPORT=ON -DUSE_MBEDTLS=ON
endif

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/lib $(1)/usr/include
	$(CP) $(PKG_BUILD_DIR)/libevmongoose.so $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/mongoose.h $(1)/usr/include
endef

define Package/evmongoose/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/libevmongoose.so $(1)/usr/lib
endef

$(eval $(call BuildPackage,evmongoose))
