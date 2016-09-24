## OSX - Tested on EI CAPITAN
Install Mac Ports
```
sudo port install git gsed gawk binutils gperf grep gettext py-serial wget libtool autoconf automake
```

```
hdiutil create -size 5g -fs "Case-sensitive HFS+" -volname ESPTools ESPTools.sparsebundle
hdiutil attach ESPTools.sparsebundle
sudo ln -s /Volumes/ESPTools/ /tools
mkdir /tools/esp8266 /tools/esp8266/sdk /tools/esp8266/compiler
cd /tools/esp8266/compiler

git clone -b lx106 git://github.com/jcmvbkbc/crosstool-NG.git 
cd crosstool-NG
sed -i.bak '1s/^/gettext=\'$'\n/' crosstool-NG/kconfig/Makefile
./bootstrap && ./configure --prefix=`pwd` && make && make install
./ct-ng xtensa-lx106-elf
./ct-ng build

```

If have nay error like `error: unknown type name 'ptrdiff_t'` please exec command  `sed -i.bak '/__need_size_t/d' .build/src/gmp-5.1.3/gmp-h.in`, then `./ct-ng build again`  (look at: https://github.com/pfalcon/esp-open-sdk/issues/45)
`nano ~/.bash_profile`

add this line:
`export PATH=$PATH:/tools/esp8266/compiler/crosstool-NG/builds/xtensa-lx106-elf/bin`
Update ENV variable
`source ~/.bash_profile`
Test: `xtensa-lx106-elf-gcc -v`

Install esptool.py 
```
cd /tools/esp8266
git clone https://github.com/themadinventor/esptool.git
```

Download lastest SDK from ... to /tools/esp8266/sdk/
Download libc, libhal, include file
```
cd /tools/esp8266/compiler/crosstool-NG/builds/xtensa-lx106-elf/xtensa-lx106-elf/sysroot/usr
wget -O lib/libc.a https://github.com/esp8266/esp8266-wiki/raw/master/libs/libc.a
wget -O lib/libhal.a https://github.com/esp8266/esp8266-wiki/raw/master/libs/libhal.a
wget -O include.tgz https://github.com/esp8266/esp8266-wiki/raw/master/include.tgz
tar -xvzf include.tgz

```
Build test:
```
cd /tools/esp8266
mkdir projects
cd projects
git clone https://github.com/tuanpmt/esp_mqtt
cd esp_mqtt
make
```

## Windows - tested on Windows 8.1

### Install SDK and tools
- Download Unofficial Development kit for Windows from: http://programs74.ru/udkew-en.html, only need xtensa-lx106-elf compiler and utils sections. It will install at C:/Espressif folder, utils at: C:\MinGW 
- Add C:\MinGW\msys\1.0\bin, C:\MinGW\bin to ENV PATH 
- Download lastest sdk from: bbs.espressif.com to c:/Espressif/sdk folder

## Linux - Ubuntu 14.04

### Cài đặt các tool
- Cài đặt phần mền hổ trợ
```
    sudo apt-get install make unrar-free autoconf automake libtool gcc g++ gperf \ flex bison texinfo gawk ncurses-dev libexpat-dev python-dev python python-serial \ sed git unzip bash help2man wget bzip2
```
- Tạo folder esp8266, sdk, compiler
```
   mkdir /opt/esp8266 /opt/esp8266/sdk /opt/esp8266/compiler 
```
- Chuyển đến folder compiler để build chương trình biên dịch
```
    cd /opt/esp8266/compiler

    git clone -b lx106 git://github.com/jcmvbkbc/crosstool-NG.git 
    cd crosstool-NG
    sed -i.bak '1s/^/gettext=\'$'\n/' crosstool-NG/kconfig/Makefile
    ./bootstrap && ./configure --prefix=`pwd` && make && make install
    ./ct-ng xtensa-lx106-elf
    ./ct-ng build
```
- Và bây giờ bạn có khoảng 30 phút, trong khi chờ build trình biên dịch
- Sau khi build xong trình biên dịch thành công, ta add dòng lệnh
`export PATH=$PATH:/tools/esp8266/compiler/crosstool-NG/builds/xtensa-lx106-elf/bin`
- Sau đó update ENV với lệnh
`source ~/.bash_profile`
- Để biết thành công hay chưa ta test với lệnh
`xtensa-lx106-elf-gcc -v`
- Cài đặt esptool.py
```
    cd /tools/esp8266
    git clone https://github.com/themadinventor/esptool.git
```
- Tải bản SDK mới nhất![ tại đây ](https://espressif.com/en/support/download/sdks-demos) để vào folder SDK tạo lúc đầu
- Tải các file: libc, libhal, include 
```
    cd /tools/esp8266/compiler/crosstool-NG/builds/xtensa-lx106-elf/xtensa-lx106-elf/sysroot/usr
    wget -O lib/libc.a https://github.com/esp8266/esp8266-wiki/raw/master/libs/libc.a
    wget -O lib/libhal.a https://github.com/esp8266/esp8266-wiki/raw/master/libs/libhal.a
    wget -O include.tgz https://github.com/esp8266/esp8266-wiki/raw/master/include.tgz
    tar -xvzf include.tgz

```
- Cuối cùng ta tải esp-8266 tại ![https://github.com/tuanpmt/esp_mqtt](https://github.com/tuanpmt/esp_mqtt) và tận hưởng thành quả
```
cd /tools/esp8266
mkdir projects
cd projects
git clone https://github.com/tuanpmt/esp_mqtt
cd esp_mqtt
make
```