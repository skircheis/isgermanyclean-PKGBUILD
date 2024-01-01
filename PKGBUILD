# Maintainer: Siegfried Kircheis < kircheis [dot] siegfried [at] proton [dot] me >

_pkgname=isgermanyclean
pkgname=${_pkgname}-git
pkgver=0.5.0.r2.g615aa9f
pkgrel=1
pkgdesc="Is Germany cleaner than France today?"
url='http://github.com/skircheis/isgermanyclean.git'
arch=('any')
license=('MIT')
depends=(
    'python>=3.9'
    'python-flask'
    'python-flask-assets'
    'python-matplotlib'
    'python-pandas'
    'sass'
    'systemd'
    'sqlite'
    'texlive-core'
    'texlive-latexextra'
    'uwsgi'
    'uwsgi-plugin-python'
)
makedepends=(
    'python-setuptools'
    'python-wheel'
    'python-versioningit'
    'python-setuptools-git'
)
source=('git+https://github.com/skircheis/isgermanyclean.git')
sha256sums=(SKIP)

provides=("${pkgname}")

pkgver() {
  cd "$srcdir/$_pkgname"
  git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
    # Clean out old wheels etc.
    git -C "${_pkgname}" clean -dfx
}

build() {
    cd "${_pkgname}"
    python -m build --wheel --no-isolation
}

package() {
    cd "${_pkgname}"
    python -m installer --destdir="$pkgdir" dist/*.whl

    mkdir -p "$pkgdir/usr/lib/systemd/user"
	install -Dm644 systemd/user/* \
		"$pkgdir/usr/lib/systemd/user"
}
