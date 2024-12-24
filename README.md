# An easy(ish) way to manage PHP deps on Windows ARM64

This uses the awesome [microsoft/vcpkg](https://github.com/microsoft/vcpkg) to gather and build most of the deps that we need using `cmake`.

A few of them are hand built from the [winlibs](https://github.com/winlibs) org. Notably `libxml2`, `readline` and `enchant`. `libxml2` is offered by `vcpkg` but it doesnt build correctly with php. The `readline` lib offered by `vcpkg` also is not sufficent for `PHP`. `enchant` does not yet exist as a port.

The `cmake` project itself is meaningless. We are simply using it as a dependency manager. clone the repo and run the following to commands from the VS Developer Prompt

- ` cmake -B build -S . -DCMAKE_TOOLCHAIN_FILE=d:/vcpkg/scripts/buildsystems/vcpkg.cmake -DVCPKG_TARGET_TRIPLET=arm64-windows-static`
- ` cmake -B build -S . -DCMAKE_TOOLCHAIN_FILE=d:/vcpkg/scripts/buildsystems/vcpkg.cmake -DVCPKG_TARGET_TRIPLET=arm64-windows`


That will gather and and build the deps necessary to build PHP

Then you can use the PHP SDK to configure and build PHP on Windows on ARM!

Ive been able to work my way up to this so far.

`configure --with-mp=12 --with-extra-libs=d:\php-deps\build\vcpkg_installed\arm64-windows-static\lib --with-extra-includes=d:\php-deps\build\vcpkg_installed\arm64-windows-static\include;d:\php-deps\build\vcpkg_installed\arm64-windows-static\include\libxml2;d:\php-deps\build\vcpkg_installed\arm64-windows-static\include\avif;d:\php-deps\build\vcpkg_installed\arm64-windows-static\include\webp;d:\php-deps\build\vcpkg_installed\arm64-windows-static\include\libpq --with-verbosity=2 --with-curl --enable-intl --with-openssl --with-enchant --enable-pdo --enable-phar-native-ssl --without-gd --with-pgsql --enable-exif --enable-mbstring --enable-mbregex --with-sqlite3 --enable-odbc --enable-apache2handler --enable-phpdbg --with-bz2 --enable-ftp`



![PHP Build Config](https://github.com/jamespack/php-deps-windows-arm64/blob/main/config.png?raw=true)

![PHP Running Locally Built](https://github.com/jamespack/php-deps-windows-arm64/blob/main/Running.png?raw=true)