# Crystal HD driver (0.9.30) installation for Ubuntu #

**Install dependencies:**
```
sudo apt-get install checkinstall git-core autoconf build-essential subversion dpkg-dev fakeroot pbuilder build-essential dh-make debhelper devscripts patchutils quilt git-buildpackage pristine-tar git yasm zlib1g-dev zlib-bin libzip-dev libx11-dev libx11-dev libxv-dev vstream-client-dev libgtk2.0-dev libpulse-dev libxxf86dga-dev x11proto-xf86dga-dev git libgstreamermm-0.10-dev libgstreamer0.10-dev automake
```
**Get source**
```
git clone git://git.linuxtv.org/jarod/crystalhd.git
```

**Fix the code for use in Ubuntu 11.10 and later**
```
insert: #include <linux/delay.h>
into : <crystalhd dir>/driver/linux/crystalhd_flea_ddr.c
```

**Compile driver**
```
cd crystalhd/driver/linux
autoconf
./configure
make
sudo make install
```
**Compile lib**
```
cd ../../linux_lib/libcrystalhd/ 
make 
sudo make install 
```
**Load driver**
```
sudo modprobe crystalhd
```
# Gstreamer-plugin installation (for use in totem i.e.) #
**Install dependencies**
```
sudo apt-get install libtool
```

**Compile plugin**
```
cd ../../filters/gst/gst-plugin/
./autogen.sh
make
sudo make install
```

**In case it doesn't compile**
```
insert #include <stdint.h> to libcrystalhd_if.h
```

**Copy the plugin files into the correct folder and run the scanner**
```
sudo cp /usr/lib/gstreamer-0.10 /usr/lib/gstreamer0.10/ -R
/usr/lib/gstreamer0.10/gstreamer-0.10/gst-plugin-scanner
```

# Enabling Adobe-flash video acceleration #
**Optional (may be needed for Ubuntu < 12.04): Replace the flashplugin with the most recent one from adobe**
```
sudo apt-get install adobe-flashplugin
```

**Generate a config file**
```
sudo mkdir /etc/adobe
sudo echo -e "EnableLinuxHWVideoDecode=1\nOverrideGPUValidation=true" > /etc/adobe/mms.cfg
```

# After Ubuntu kernel update #

**Reinstall the driver**
```
cd crystalhd/driver/linux
sudo make install
```


# Further reading #
  * http://www.mythtv.org/wiki/Broadcom_Crystal_HD#Obtaining_drivers mythtv crystalhd howto
  * http://geekparadise.de/tag/vlc/ geekparadise crystalhd howto (german)

# Troubleshooting #
Please deliver the output of "dmesg | grep crystalhd" with your description of the problem.