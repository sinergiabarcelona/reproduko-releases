# reproduko

reproduko es un reproductor de audio y vídeo gratuito, al estilo de VLC.

Sitio web: [reproduko.com](https://reproduko.com)

Este repositorio **no contiene el código de la aplicación**. Solo publica las descargas de Linux y las fuentes LGPL del motor de reproducción (libmpv y FFmpeg) que hay que ofrecer junto a esos paquetes.

## Descargas (Linux x86_64)

La versión actual es [reproduko 0.1.28](https://github.com/sinergiabarcelona/reproduko-releases/releases/tag/v0.1.28):

| Archivo | Qué es |
|---|---|
| `reproduko-0.1.28-x86_64.AppImage` | AppImage portátil (libmpv LGPL propio) |
| `reproduko-0.1.28-linux-x86_64.tar.gz` | Carpeta portable o instalación de usuario, sin root |
| `reproduko-0.1.28-x86_64.flatpak` | Paquete Flatpak (mismo libmpv LGPL) |
| `reproduko-libmpv-lgpl-linux-fuentes-0.1.28.tar.gz` | Fuentes exactas de libmpv, FFmpeg y el resto de componentes, script de compilación y configuración usada |
| `SHA256SUMS.txt` | Sumas SHA-256 de los archivos anteriores |

Hace falta glibc 2.35 o posterior (Ubuntu 22.04, Debian 12, Fedora 36, openSUSE Leap 15.5 o Tumbleweed, y versiones más nuevas). En un escritorio habitual ya están las bibliotecas de sistema que usa el AppImage y el tar.gz: GTK 3, libepoxy, libEGL, libGLESv2, libva, libvdpau, libX11, OpenSSL 3, PulseAudio o ALSA, fontconfig y zlib.

Comprueba las descargas con:

```sh
sha256sum -c SHA256SUMS.txt
```

### AppImage

No hace falta libfuse2 (lleva el runtime type2):

```sh
chmod +x reproduko-0.1.28-x86_64.AppImage
./reproduko-0.1.28-x86_64.AppImage
```

### tar.gz

```sh
tar -xzf reproduko-0.1.28-linux-x86_64.tar.gz
cd reproduko-0.1.28-linux-x86_64
./reproduko
```

Para añadirla al menú del usuario (sin root):

```sh
./instalar.sh
```

Para quitarla del menú (la carpeta no se borra): `./instalar.sh --quitar`.

### Flatpak

El paquete usa el runtime `org.freedesktop.Platform` 25.08 (Flathub):

```sh
flatpak remote-add --if-not-exists --user flathub https://flathub.org/remote-config/flathub.flatpakrepo
flatpak install --user flathub org.freedesktop.Platform//25.08
flatpak install --user reproduko-0.1.28-x86_64.flatpak
flatpak run barcelona.sinergia.reproduko
```

## Licencias

- La aplicación reproduko se distribuye bajo la [Mozilla Public License 2.0](https://mozilla.org/MPL/2.0/).
- El AppImage, el tar.gz y el Flatpak llevan un `libmpv.so.2` propio compilado como LGPL-2.1+: mpv 0.41.0 y FFmpeg 8.0.3, sin `--enable-gpl`, `--enable-nonfree` ni `--enable-version3`, y sin los decodificadores TrueHD, MLP, VVC, E-AC-3 ni DTS. El texto de la GNU Lesser General Public License 2.1 está en [LGPL-2.1.txt](LGPL-2.1.txt).
- Las fuentes completas de ese libmpv (mpv, FFmpeg, el resto de componentes, el script de compilación `libmpv-lgpl.sh` y la configuración usada) están en `reproduko-libmpv-lgpl-linux-fuentes-0.1.28.tar.gz`, en la misma release que los paquetes.

Puedes sustituir `libmpv.so.2` por otra versión compatible (reproduko lo carga como biblioteca dinámica). En el AppImage, extrae el contenido con `--appimage-extract` y cambia `squashfs-root/usr/lib/reproduko/lib/libmpv.so.2`.
