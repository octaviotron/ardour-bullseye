# ardour-bullseye
## Ardour 5.12 en Debian Bullseye

Descargar el TAR desde https://community.ardour.org/srctar

```bash

$ su -
# apt update && apt upgrade
# apt install libboost-dev libboost1.67-dev libglibmm-2.4-dev libsigc++-2.0-dev libtag1-dev \
    vamp-plugin-sdk libudev-dev libfftw3-bin libfftw3-dev libfftw3-long3 libfftw3-quad3 \
    libaubio-dev libaubio5 libusb-1.0-0-dev libpangomm-1.4-dev libsamplerate0-dev  lv2-dev \
    libserd-dev libsord-dev libsratom-dev liblilv-dev libgtkmm-2.4-dev libsuil-dev libreadline6-dev \
    itstool
```

Compilación
```bash
tar xjf Ardour-5.12.0.tar.bz2
cd Ardour-5.12.0
```
