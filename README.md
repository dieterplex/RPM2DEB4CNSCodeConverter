RPM2DEB4CNSCodeConverter
========================

This repository provide an encoded debian packages shar converted from [全字庫單機版轉碼工具(Linux版) 100.1版](http://www.cns11643.gov.tw/AIDB/download_en.do?name=%E5%80%8B%E4%BA%BA%E9%9B%BB%E8%85%A6%E9%80%A0%E5%AD%97%E8%99%95%E7%90%86%E5%B7%A5%E5%85%B7%3EUnicode%E5%B9%B3%E5%8F%B0)

This is ONLY tested in `Ubuntu 12.04` from vagrant.

Usage
-----

    wget https://github.com/dieterplex/RPM2DEB4CNSCodeConverter/raw/master/cnscodeconvertor-100-1.linux.deb.sh | sh

DIY
---

You can re-package RPM to DEB manually using `alien`.
These packages are 32bit binary, so it can be build on a 32-bit enviroment only.

    sudo apt-get -y install alien shared-mime-info desktop-file-utils libgtk2.0-0
    wget "http://www.cns11643.gov.tw/AIDB/file.do?path=download%2F%E5%80%8B%E4%BA%BA%E9%9B%BB%E8%85%A6%E9%80%A0%E5%AD%97%E8%99%95%E7%90%86%E5%B7%A5%E5%85%B7%601q%60Unicode%E5%B9%B3%E5%8F%B0%601q%60%E5%85%A8%E5%AD%97%E5%BA%AB%E5%96%AE%E6%A9%9F%E7%89%88%E8%BD%89%E7%A2%BC%E5%B7%A5%E5%85%B7%28Linux%E7%89%88%29%2Fname%2Fcnscodeconvertor-100-1.linux.sh" -O - | head -n-1 | sh
    # 1. build and install or
    sudo alien -cdiv *.rpm
    # 2. generate, modify and then build .deb by `debian/rules binary` on each package folder.
    sudo alien -cdgv *.rpm

If you use vagrant, just:

    vagrant up cnstooltest
    scp -P 2222 vagrant@127.0.0.1:*.deb ./
