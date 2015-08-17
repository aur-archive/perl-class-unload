# Maintainer: Maxwell Pray a.k.a. Synthead <synthead@gmail.com>

pkgname=perl-class-unload
_cpanname="Class-Unload"
pkgver=0.07
pkgrel=2
pkgdesc="Unload a class"
arch=('any')
license=('PerlArtistic' 'GPL')
options=('!emptydirs')
depends=('perl>=5.5.0' 'perl-class-inspector')
url="http://search.cpan.org/dist/$_cpanname"
source=("http://search.cpan.org/CPAN/authors/id/I/IL/ILMARI/$_cpanname-$pkgver.tar.gz")
md5sums=('c6a7fd628bf7a48c3374747257eb90ad')

# Function to change to the working directory and set
# environment variables to override undesired options.
prepareEnvironment() {
	cd "$srcdir/$_cpanname-$pkgver"
	export \
		PERL_MM_USE_DEFAULT=1 \
		PERL_AUTOINSTALL=--skipdeps \
		PERL_MM_OPT="INSTALLDIRS=vendor DESTDIR='$pkgdir'" \
		PERL_MB_OPT="--installdirs vendor --destdir '$pkgdir'" \
		MODULEBUILDRC=/dev/null
}

build() {
	prepareEnvironment
	/usr/bin/perl Makefile.PL
	make
}

check() {
	prepareEnvironment
	make test
}

package() {
	prepareEnvironment
	make install

	# Remove "perllocal.pod" and ".packlist".
	find "$pkgdir" -name .packlist -o -name perllocal.pod -delete
}
