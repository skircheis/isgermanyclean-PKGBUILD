# Maintainer: Siegfried Kircheis < kircheis [dot] siegfried [at] proton [dot] me >

pkgbase=isgermanyclean
pkgname=${pkgbase}-git
pkgver=0.1.0.r0.g886fb38
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
    'systemd'
    'texlive'
    'texlive-latexextra'
    'uwsgi'
    'uwsgi-plugin-python'
)
makedepends=(
    'python-setuptools'
    'python-wheel'
)
source=('git+https://github.com/skircheis/isgermanyclean.git')
sha256sums=(SKIP)

provides=("${pkgname}")

pkgver() {
  cd "$srcdir/$pkgbase"
  git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
    cd "${pkgbase}"
    python -m build --wheel --no-isolation
}

package() {
    cd "${pkgbase}"
    python -m installer --destdir="$pkgdir" dist/*.whl

    mkdir -p "$pkgdir/usr/lib/systemd/user"
	install -Dm644 systemd/user/* \
		"$pkgdir/usr/lib/systemd/user"
}
