# Maintainer: Benjamin Marwell <bmarwell@gmail.com>

pkgname=musescore-git
pkgver=3.7.0.git.1659694499.8815d554248900ca3604172d7b2664b4d1962b4f
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
conflicts=('musescore' 'musescore-git')
provides=('musescore')
install=musescore.install
_branch=master-to-3.x
source=(git+https://github.com/Jojo-Schmitz/MuseScore#branch=${_branch})
md5sums=('SKIP')

pkgver() {
  cd MuseScore
  commit=$(git show -s --format=%ct.%H HEAD)
  echo "3.7.0.git.$commit"
}

build() {
  cmake -S MuseScore -B build \
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
  cd MuseScore
  make DESTDIR="${pkgdir}" SUFFIX="-git" LABEL="Git Build" install -C build.release
}

# vim: ts=2 sw=2 et:
