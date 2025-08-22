include $(TOPDIR)/rules.mk

PKG_NAME:=hello
PKG_VERSION:=1.0.0
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/hello
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Hello World C++ program
  MAINTAINER:=Truong <999vantruong@gmail.com>
endef

define Package/hello/description
  A simple C++ Hello World program packaged for OpenWrt.
endef

# Copy your project files into the OpenWrt build directory
define Build/Prepare
    mkdir -p $(PKG_BUILD_DIR)
    $(CP) ./Hello_World/* $(PKG_BUILD_DIR)/
endef

# Compile with include path set to your inc/ folder
define Build/Compile
    $(TARGET_CXX) $(TARGET_CXXFLAGS) \
        -I$(PKG_BUILD_DIR)/inc \
        $(PKG_BUILD_DIR)/src/*.cpp \
        $(PKG_BUILD_DIR)/main.cpp \
        -o $(PKG_BUILD_DIR)/hello
endef

# Install binary into /usr/bin on the target
define Package/hello/install
    $(INSTALL_DIR) $(1)/usr/bin
    $(INSTALL_BIN) $(PKG_BUILD_DIR)/hello $(1)/usr/bin/
endef

$(eval $(call BuildPackage,hello))
