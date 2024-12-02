Vagrant.configure("2") do |config|

  config.vm.define "dockerhost" do |harry_dockerhost|
    harry_dockerhost.vm.box = "generic/debian12"
    harry_dockerhost.vm.network "public_network"
    harry_dockerhost.vm.network "private_network", ip: "10.10.10.130", virtualbox__intnet: "ansible_harry"
    harry_dockerhost.vm.hostname = "harry-dockerhost"
    harry_dockerhost.vm.provider :virtualbox do |vb|
      vb.memory = 4096
      vb.cpus = 2
      vb.name = "harry-dockerhost"
    end
    harry_dockerhost.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y git snmpd tmux mc wget tree
	  sudo apt install apt-transport-https ca-certificates curl gnupg
	  curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker.gpg
	  echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker.gpg] https://download.docker.com/linux/debian bookworm stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
	  sudo apt update
	  sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
	  sudo usermod -aG docker vagrant
    SHELL
  end
config.vm.define "ansible" do |harry_ansible|
  harry_ansible.vm.box = "generic/debian12"
  harry_ansible.vm.network "public_network"
  harry_ansible.vm.network "private_network", ip: "10.10.10.131", virtualbox__intnet: "ansible_harry"
  harry_ansible.vm.hostname = "harry-ansible"
  harry_ansible.vm.synced_folder "./ansible_harry", "/vagrant_data"
  harry_ansible.vm.provider :virtualbox do |vb|
    vb.memory = 2048
    vb.cpus = 1
	vb.name = "harry-ansible"
    end
	harry_ansible.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y git ansible sshpass yamllint ansible-lint
    SHELL
  end
config.vm.define "ubuntu" do |harry_ubuntu|
  harry_ubuntu.vm.box = "bento/ubuntu-24.04"
  harry_ubuntu.vm.network "public_network"
  harry_ubuntu.vm.network "private_network", ip: "10.10.10.132", virtualbox__intnet: "ansible_harry"
  harry_ubuntu.vm.hostname = "harry-ubundu"
  harry_ubuntu.vm.provider :virtualbox do |vb|
    vb.memory = 2048
    vb.cpus = 1
    vb.name = "harry-ubundu"
  end
  harry_ubuntu.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y git snmpd tmux mc wget tree
  SHELL
end
config.vm.define "centos" do |harry_centos|
  harry_centos.vm.box = "generic/centos9s"
  harry_centos.vm.network "public_network"
  harry_centos.vm.network "private_network", ip: "10.10.10.133", virtualbox__intnet: "ansible_harry"
  harry_centos.vm.hostname = "harry-centos"
  harry_centos.vm.provider :virtualbox do |vb|
    vb.memory = 2048
    vb.cpus = 1
	vb.name = "harry_centos"
	end
	  harry_centos.vm.provision "shell", inline: <<-SHELL
    dnf update
    dnf install -y git tmux mc wget tree net-snmp net-snmp-utils
      sudo sed -i "/^[^#]*PasswordAuthentication[[:space:]]no/c\PasswordAuthentication yes" /etc/ssh/sshd_config
      sudo systemctl restart sshd
  SHELL
    end
config.vm.define "opensuse" do |harry_opensuse|
  harry_opensuse.vm.box = "bento/opensuse-leap-15"
  harry_opensuse.vm.network "public_network"
  harry_opensuse.vm.network "private_network", ip: "10.10.10.134", virtualbox__intnet: "ansible_harry"
  harry_opensuse.vm.hostname = "harry-opensuse"
  harry_opensuse.vm.provider :virtualbox do |vb|
    vb.memory = 2048
    vb.cpus = 1
	vb.name = "harry-opensuse"
	 end
  harry_opensuse.vm.provision "shell", inline: <<-SHELL
    zypper update
    zypper install -y git net-snmpd tmux mc wget tree
  SHELL
end
end