### This is for rpm-ostree based system

```
# Clone repo
git clone https://github.com/catsout/wallpaper-engine-kde-plugin.git
cd wallpaper-engine-kde-plugin


# Install plugin package 
# plasmapkg2 -u, for update
plasmapkg2 -i ./plugin

mkdir -p $HOME/rpmbuild/SOURCES

# Install build dependencies (in distrobox)

sudo dnf install vulkan-headers plasma-workspace-devel kf5-plasma-devel gstreamer1-libav lz4-devel mpv-libs-devel python3-websockets qt6-qtbase-private-devel qt5-qtx11extras-devel qt6-qtwebchannel-devel qt6-qtwebsockets-devel cmake ninja

# Rpmbuild in distrobox
rpmbuild --define="commit $(git rev-parse HEAD)" \
    --define="glslang_ver 11.8.0" \
    --undefine=_disable_source_fetch \
    -ba ./rpm/wek.spec

# Install package
cd ~/rpmbuild/RPMS/x86_64
rpm-ostree install --uninstall=wallpaper-engine-kde-plugin ./<select-rpm-to-install>.rpm
```
