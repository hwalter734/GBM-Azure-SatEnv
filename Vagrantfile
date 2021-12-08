Vagrant.configure("2") do |config|
  config.vm.define "Tower" do |ansible1|
    ansible1.vm.box = "centos/7"
    ansible1.vm.hostname = "RedHat.hl.local"
    ansible1.vm.network "private_network", ip: "{{ ansible_default_ipv4.address }}"
    ansible1.vm.disk :disk, size: '50GB', primary: true
    ansible1.vm.provision "shell",
      inline: "echo hello from ansible1"
    ansible1.vm.provision "shell", inline: <<-SHELL
      sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config    
      systemctl restart sshd.service
      sudo yum install -y python3-pip
      sudo pip3 install ansible 
      #echo export PATH=$PATH:$HOME/.local/bin >> ~/.bashrc
      #source ~/.bashrc
      sudo yum install -y wget
      wget https://releases.ansible.com/ansible-tower/setup/ansible-tower-setup-latest.tar.gz
      tar -xvf ansible-tower-setup-latest.tar.gz
      sudo chown -R vagrant:vagrant /home/vagrant
      sed -i "s/admin_password=''/admin_password='ansible'/g" ansible-tower-*/inventory
      sed -i "s/pg_password=''/pg_password='ansible'/g" ansible-tower-*/inventory
      whoami > result.txt
      runuser -l root -c '/home/vagrant/ansible-tower-setup-*/setup.sh'
      rm -Rf /home/vagrant/ansible-tower*
    SHELL
    ansible1.vm.provider :virtualbox do |vb|
      vb.memory = 6024
      vb.cpus = 2
      vb.name = "Tower"
      unless File.exist?('./sdb5.1.vdi')
        vb.customize ['createhd', '--filename', './sdb5.1.vdi', '--variant', 'Fixed', '--size', 1 * 1024]
      end
      vb.customize ['storageattach', :id,  '--storagectl', 'IDE', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', './sdb5.1.vdi']
    end
  end

end
