Vagrant.configure("2") do |config|
  config.vm.define "admvm" do |admvm|
    admvm.vm.hostname = "admvm"
    admvm.vm.box = "ubuntu/focal64"
    admvm.vm.network "private_network", ip: "192.168.33.10"
    admvm.vm.network "forwarded_port", guest: 80, host: 8888


    admvm.vm.provider "virtualbox" do |vb|
      vb.name = "admvm"
      vb.gui = false
      vb.memory = "1024"
    end

    admvm.vm.provision "shell", run: "always",  inline: <<-SHELL
        echo "Hello from the Ubuntu VM"
        sudo useradd -m adminuser
        echo 'adminuser:&^LmBcpY44hul#5uLlmzosTi!6AuvB*nh22jJjB14Vp*m3XSVS' | sudo chpasswd
        sudo usermod -a -G admin adminuser
        sudo useradd -m poweruser
        sudo passwd -d poweruser
        echo 'poweruser ALL=(ALL) NOPASSWD: /usr/sbin/iptables' | sudo EDITOR='tee -a' visudo
        
        sudo usermod -a -G adminuser poweruser
        
        sudo ln -s /etc/mtab /home/poweruser/mylink
    SHELL
  end
  
end
