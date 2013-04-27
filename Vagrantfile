# -*- mode: ruby -*-
# vi: set ft=ruby :

# How to test:
#   vagrant up cnstooltest64 # or cnstooltest
#   ssh -Y vagrant@127.0.0.1 -p2222 cnscodeconvertor
#   open /vagrant/Big5Sample.html.
#   output as unicode or else.

Vagrant::Config.run do |config|

  config.vm.define :cnstooltest do |hq|
    hq.vm.box     = 'precise32'
    hq.vm.box_url = 'http://files.vagrantup.com/precise32.box'
    hq.vm.customize [ "modifyvm", :id , "--name", "cnstooltest"]

    $script = <<-SCRIPT.gsub /^\s+/, ""
        export DEBIAN_FRONTEND=noninteractive
        cp -f /vagrant/sources.list /etc/apt # Taiwan mirror site
        apt-get -q update

        apt-get -y install alien shared-mime-info desktop-file-utils libgtk2.0-0
        install -d ~vagrant/cnsfiles && (
        cd ~vagrant/cnsfiles;
        wget "http://www.cns11643.gov.tw/AIDB/file.do?path=download%2F%E5%80%8B%E4%BA%BA%E9%9B%BB%E8%85%A6%E9%80%A0%E5%AD%97%E8%99%95%E7%90%86%E5%B7%A5%E5%85%B7%601q%60Unicode%E5%B9%B3%E5%8F%B0%601q%60%E5%85%A8%E5%AD%97%E5%BA%AB%E5%96%AE%E6%A9%9F%E7%89%88%E8%BD%89%E7%A2%BC%E5%B7%A5%E5%85%B7%28Linux%E7%89%88%29%2Fname%2Fcnscodeconvertor-100-1.linux.sh" -O - | head -n-1 | sh
        )
        sudo alien -cdiv ~vagrant/cnsfiles/*.rpm
        apt-get -y install fonts-cns11643-kai fonts-cns11643-sung fontforge default-jre libqtcore4 libqtgui4

        mkdir -p /usr/lib/jvm/default-java/jre/lib/fonts/fallback
        ln -s /usr/share/fonts/truetype/cns11643/* /usr/lib/jvm/default-java/jre/lib/fonts/fallback

        #sh /vagrant/cnscodeconvertor-100-1.linux.deb.sh
    SCRIPT
    hq.vm.provision :shell, :inline => $script

  end

  config.vm.define :cnstooltest64 do |hq|
    hq.vm.box     = 'precise64'
    hq.vm.box_url = 'http://files.vagrantup.com/precise64.box'

    hq.vm.customize [ "modifyvm", :id , "--name", "cnstooltest64"]

    $script = <<-SCRIPT.gsub /^\s+/, ""
        export DEBIAN_FRONTEND=noninteractive
        cp -f /vagrant/sources.list /etc/apt # Taiwan mirror site
        apt-get -q update

        apt-get -y install fonts-cns11643-kai fonts-cns11643-sung default-jre
        mkdir -p /usr/lib/jvm/default-java/jre/lib/fonts/fallback
        ln -s /usr/share/fonts/truetype/cns11643/* /usr/lib/jvm/default-java/jre/lib/fonts/fallback

        sh /vagrant/cnscodeconvertor-100-1.linux.deb.sh
    SCRIPT
    hq.vm.provision :shell, :inline => $script

  end
end
