Vagrant.configure("2") do |config|
  config.vm.define "adminmisha" do |adminmisha|
    adminmisha.vm.hostname = "adminmisha"
    adminmisha.vm.box = "ubuntu/focal64"
    adminmisha.vm.network "private_network", ip: "192.168.33.10"
    adminmisha.vm.network "forwarded_port", guest: 80, host: 8888


    adminmisha.vm.provider "virtualbox" do |vb|
      vb.name = "adminmisha"
      vb.gui = false
      vb.memory = "1024"
    end

    adminmisha.vm.provision "shell", run: "always",  inline: <<-SHELL
        echo "Hello from the Ubuntu VM"
        sudo useradd -m  -p '$6$enterpass$LWikCV49XN.urs/pEkh9n2Nk3nyL6O9jeAwKat3F/qbArFJqdHKnEFAdDuhKWWSDpc/vZWkQ5V.eEec.m/z5X.' adminuser
        sudo usermod -a -G admin adminuser
        sudo useradd -m poweruser
        sudo passwd -d poweruser
        echo 'poweruser ALL=(ALL) NOPASSWD: /usr/sbin/iptables' | sudo EDITOR='tee -a' visudo
        sudo usermod -a -G adminuser poweruser
        sudo ln -s /etc/mtab /home/poweruser/mylink
    SHELL
  end
  
end
