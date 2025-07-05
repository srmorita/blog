+++
date = '2025-07-04T20:33:00-04:00'
draft = false
slug = 'primeros-pasos-tras-una-instalacion-experta-en-debian'
title = 'Primeros pasos tras una instalación experta en Debian'
description = "Primeros pasos tras una instalación experta en Debian"
keywords = ['debian, gnu, linux']
+++
Uno de mis sistemas __GNU/Linux__ favorito es [Debian](https://www.debian.org/ "Debian Website") y cada vez que lo instalo casi siempre realizo los mismos pasos y la verdad nunca lo he compartido así que aquí te dejo una mini guía de lo que hago tras instalar _Debian_.

__DISCLAIMER__, esto asume que realizaste una instalación experta y solo instalaste las _utilidades estandar del sistema_ en una versión Debian 12.

### Agregar usuario al sudoers file

Necesitamos agregar nuestro usuario al archivo sudoers para poder usar el comando _sudo_ (si seleccionaste en la instalación no permitir el ingreso como root, puedes omitir este paso)

```bash
su - root // nos logueamos como root e ingresamos contraseña

usermod -aG sudo tuUsuario // cambia tuUsuario por el tuyo obviamente XD

reboot // reiniciamos
```

### Herramientas de compilación

Instalar software para compilar lo que necesites:

```bash
sudo apt -y install build-essential checkinstall make automake cmake autoconf
```

y no olvidar los headers del kernel:

```bash
sudo apt -y install linux-headers-$(uname -r)
```

### Mejorar nuestro `/etc/apt/sources.list`

Este es un archivo importante, ya que, es donde se configuran nuestros repositorios de software. Me gusta indicar la arquitectura de mi ordenador para así optimizar recursos y no descargar archivos innecesarios, además de utilizar solo la rama _stable_ (esto es a gusto de cada quien) y mantenerlo lo más limpio posible. No uso el repositorio de [deb-multimedia](https://deb-multimedia.org/ "deb-multimedia website") porque en el repo _non-free_, ya tengo lo necesario. Tampoco uso _backports_.

```bash
deb [arch=amd64] http://ftp.cl.debian.org/debian/ stable main contrib non-free non-free-firmware
deb [arch=amd64] http://security.debian.org/debian-security stable-security main contrib non-free non-free-firmware
deb [arch=amd64] http://ftp.cl.debian.org/debian/ stable-updates main contrib non-free non-free-firmware
```

En el repositorio security podemos tener algunos problemas de sincronización si es que no hemos configurado correctamente la zona horaria en nuestro equipo, se resuelve configurando __ntp__ o en mi caso prefiero usar _systemd-timesyncd_

```bash
sudo systemctl enable systemd-timesyncd
```

Y reinicia...

### Firmware

Este apartado siempre es necesario, por lo general, el kernel linux soporta infinidad de hardware y probablemente funcione _out-of-the-box_, salvo el microcode y el firmware de nuestra tarjeta gráfica me refiero a _AMD_ o _NVIDIA_ (intel está muy bien soportado y solo necesitas intalar el microcode).

#### AMD Microcode y drivers gráficos

```bash
sudo apt install amd64-microcode firmware-amd-graphics libgl1-mesa-dri libglx-mesa0 mesa-vulkan-drivers xserver-xorg-video-amdgpu
```

#### INTEL Microcode y drivers gráficos

```bash
sudo apt install intel-microcode xserver-xorg-video-intel
```

#### WIFI

Para el _wifi_, basta con:

```bash
sudo apt install firmware-iwlwifi
```

### Audio

Para el audio tenemos [_ALSA_](https://www.alsa-project.org/wiki/Main_Page "ALSA Website") y viene por defecto en el kernel, podemos instalar aparte las utilidades con:

```bash
sudo apt install alsa-utils
```

[Pipewire](https://wiki.debian.org/PipeWire#Installation "Pipewire Debian") es un servidor y API para manejar multimedia en Debian y a día de hoy y según mi opinion deberias usarlo sí o sí.

```bash
sudo apt install pipewire-audio wireplumber pipewire-pulse pipewire-alsa
```

### Entorno de escritorio

Tenemos muchas opciones acá, me limito a lo que yo suelo usar/instalar que es _Gnome_ y _XFCE_.

#### Gnome

```bash
sudo apt install gnome-core gdm
```

#### XFCE

```bash
sudo apt install xfce4 xfce4-goodies gvfs-backends ttf-bitstream-vera lightdm lightdm-gtk-greeter pavucontrol network-manager-gnome
```

Para que _NetworkManager_ gestione nuestras conexiones de red, modificamos el archivo `/etc/NetworkManager/NetworkManager.conf`:

```bash
sudo nano /etc/NetworkManager/NetworkManager.conf
```

Y cambiamos a true la variable managed bajo _[ifupdown]_

```bash
[ifupdown]
managed=true
```

Y reiniciamos network manager:

```bash
sudo systemctl restart network-manager
```

Con esto ya tienes un entorno mínimo funcional y puedes comenzar a jugar con tu Debian!!!

EOF.
