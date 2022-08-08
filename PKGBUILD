# Maintainer: Benjamin Marwell <bmarwell@gmail.com>

pkgname=musescore-3.7-git
pkgver=r19763.8815d55424
pkgrel=1
pkgdesc='Create, play and print beautiful sheet music (unreleased git 3.7 branch)'
arch=(x86_64)
url='https://github.com/musescore/MuseScore'
license=('GPL')
groups=(pro-audio)
depends=(
  alsa-lib
  freetype2
  libpulse
  libsndfile
  libvorbisfile.so
  portaudio
  portmidi
  libportaudio.so
  libportmidi.so
  qt5-base
  qt5-declarative
  qt5-graphicaleffects
  qt5-quickcontrols
  qt5-quickcontrols2
  qt5-svg
  qt5-tools
  qt5-webengine
  qt5-xmlpatterns
  zlib
)
makedepends=(
  cmake
  doxygen
  git
  lame
  qt5-script
  texlive-core
)
optdepends=('lame: MP3 export')
conflicts=('musescore')
provides=('musescore')
_branch=master-to-3.x
source=("MuseScore-Jojo-Schmitz::git+https://github.com/Jojo-Schmitz/MuseScore#branch=${_branch}")
md5sums=('SKIP')

pkgver() {
  cd MuseScore-Jojo-Schmitz
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
  cmake -S MuseScore-Jojo-Schmitz -B build \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_SKIP_RPATH=ON \
    -DBUILD_CRASH_REPORTER=OFF \
    -DBUILD_TELEMETRY_MODULE=OFF \
    -DBUILD_WEBENGINE=OFF \
    -DDOWNLOAD_SOUNDFONT=OFF \
    -DMUSESCORE_BUILD_CONFIG=release \
    -DMUSESCORE_REVISION=$(git rev-parse --short=7 HEAD) \
    -DPACKAGE_FILE_ASSOCIATION=ON \
    -DUSE_SYSTEM_FREETYPE=ON \
    -Wno-dev
  make lrelease manpages -C build;
  make -C build;
}

package() {
  make DESTDIR="${pkgdir}" LABEL="Git Build" install -C build
}

# vim: ts=2 sw=2 et:
