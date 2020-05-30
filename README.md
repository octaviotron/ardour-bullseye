# Compilación de Ardour 6 para Debian Bullseye

```
Por Octavio Rossell <octavio@gnu.org.ve>
Licencia CC-BY-SA
```

En la actualidad (30 mayo de 2020) no existe un paquete instalable del DAW Ardour para Debian Bullseye. Este pequeño tutorial instruye cómo obtenerlo y correr esta muy necesaria herramienta para aquellos a quienes nos gusta la producción de audio profesional en GNU/Linux.

## Instalación de Dependencias

```bash
apt update && apt upgrade
apt install libboost-dev libboost1.67-dev libglibmm-2.4-dev libsigc++-2.0-dev libtag1-dev \
    vamp-plugin-sdk libudev-dev libfftw3-bin libfftw3-dev libfftw3-long3 libfftw3-quad3 \
    libaubio-dev libaubio5 libusb-1.0-0-dev libpangomm-1.4-dev libsamplerate0-dev  lv2-dev \
    libserd-dev libsord-dev libsratom-dev liblilv-dev libgtkmm-2.4-dev libsuil-dev libreadline6-dev \
    itstool build-essential libcanberra-gtk-module libcanberra-gtk0 libwebsockets-dev
```

## Obtención del Software

La mejor vía para obtener el código fuente es a través de la descarga del TAR desde https://community.ardour.org/srctar. Hay una vía alterna usando el repositorio GIT, pero de esta manera se obtendrá la versión de desarrollo, a la cual se le realizan cambios diariamente y hay una alta probablilidad de hacerse con librerías que estén rotas o con bugs que se están arreglando mientras compilamos, así que:

Como usuario regular (nada de root por lo pronto) ejecutamos:

```bash
wget https://community.ardour.org/srctar -O Ardour-6.0.0.tar.bz2
tar -xjf Ardour-6.0.0.tar.bz2
cd Ardour-5.0.0
```

Pera el momento de creación de este documento, la última versión estable es la 6.0.0. Es posible que el comando anterior requiera ajustar la ruta si cambia el nombre del directorio que se crea al descomprimir el .tar.bz2

## Compilación

Preparamos el entorno de compilación:

```bash
./waf configure --program-name=ardour6 --with-backends=jack,alsa,pulseaudio --freedesktop --lxvst --progress --canvasui
```
Se configura con la banderas (flags) **--program-name** para determinar el nombre del binario resultante, **--with-backends=jack,alsa** para añadir soportes para JACK, ALSA y PULSEAUDIO, **--freedesktop** para que se generen los archivos .desktop que pueden ser posteriormente añadidos al manejador de ventanas, **--canvasui** para añadir soporte para la interfaz gráfica mediante la librería "libcanvas", **--lxvst** para el soporte de plugins VST compilados para GNU/Linux y **--progress** para que muestre una barra de progreso al compilar (esto último es opcional)

Finalmente procedemos a compilar:
```bash
./waf
```

## Instalando en el sistema

Hasta este punto ya Ardour es usable. En el directorio "gtk2_ardour" que se ha creado durante la compilación hay un binario llamado "ardev" el cual al ejecutarlo se abre la aplicación, pero ya va:

Ahora si, como root:
```bash
su
./waf install
exit
```

Y ¡listo! como hemos llamado "ardour5" a nuestro programa (flag --program-name) ejecutamos en una cónsola:

```bash
ardour5
```

Ahora bien, si queremos usar un ícono en el menú de nuestro WM preferido:
```bash
su
cp ./build/gtk2_ardour/ardour5.desktop /usr/share/applications/
cp /usr/local/share/ardour5/icons/application-x-ardour_48px.png /usr/local/share/ardour5/icons/ardour5-icon_48px.png
cp /usr/local/share/ardour5/icons/application-x-ardour_16px.png /usr/local/share/ardour5/icons/ardour5-icon_16px.png
cp /usr/local/share/ardour5/icons/application-x-ardour_22px.png /usr/local/share/ardour5/icons/ardour5-icon_22px.png
cp /usr/local/share/ardour5/icons/application-x-ardour_32px.png /usr/local/share/ardour5/icons/ardour5-icon_32px.png
exit
```

Mola un montón compilar nuestras propias aplicaciones preferidas en Software Libre: ¿si o qué?


