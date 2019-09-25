Vagrant.configure("2") do |config|
  
  ##
  ##
  ##  Puppet
  ##
  ##
  config.vm.box = "ubuntu/bionic64"

  ##
  ## se debe ejecutar en el prompt
  ##
  ##    vagrant plugin install vagrant-disksize
  ##
  config.disksize.size = '15GB'

  config.vm.provider "virtualbox" do |v|
    v.memory = 12248
    v.cpus = 4
  end

  config.vm.provision "shell", inline: <<-SHELL

    sudo apt-get update 

    sudo apt-get install -yq \
      build-essential \
      tree \
      apt-transport-https \
      ca-certificates \
      curl \
      gnupg-agent \
      software-properties-common

    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    
    sudo add-apt-repository \
      "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
      $(lsb_release -cs) \
      stable"

    sudo apt-get update

    sudo apt-get install -yq \
      docker-ce=5:19.03.1~3-0~ubuntu-bionic \
      docker-ce-cli=5:19.03.1~3-0~ubuntu-bionic \
      containerd.io

    sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" \
      -o /usr/local/bin/docker-compose

    sudo chmod +x /usr/local/bin/docker-compose

    sudo curl -L https://raw.githubusercontent.com/docker/compose/1.24.1/contrib/completion/bash/docker-compose \
      -o /etc/bash_completion.d/docker-compose

    rm -rf /var/lib/apt/lists/*

  SHELL

  ## Open Refine
  config.vm.network :forwarded_port, guest: 3333, host: 3333, host_ip: "127.0.0.1"

  ## Jupyter
  config.vm.network :forwarded_port, guest: 8888, host: 8888, host_ip: "127.0.0.1"
  config.vm.network :forwarded_port, guest: 5000, host: 5000, host_ip: "127.0.0.1"

  ## TensorBoard
  config.vm.network :forwarded_port, guest: 8000, host: 8000, host_ip: "127.0.0.1"
  config.vm.network :forwarded_port, guest: 6006, host: 6006, host_ip: "127.0.0.1"

  ## Hadoop 2.8.5
  config.vm.network :forwarded_port, guest: 9000,   host: 9000,  host_ip: "127.0.0.1"  # dfs 
  config.vm.network :forwarded_port, guest: 50070,  host: 50070, host_ip: "127.0.0.1"  # NameNode
  config.vm.network :forwarded_port, guest: 8088,   host: 8088,  host_ip: "127.0.0.1"  # Yarn 

  ## Zeppelin
  config.vm.network :forwarded_port, guest: 8080,   host: 8080,  host_ip: "127.0.0.1"  

  ## Spark UI
  config.vm.network :forwarded_port, guest: 8881,   host: 8881,  host_ip: "127.0.0.1"
  config.vm.network :forwarded_port, guest: 8880,   host: 8880,  host_ip: "127.0.0.1"
  config.vm.network :forwarded_port, guest: 4040,   host: 4040,  host_ip: "127.0.0.1"
  config.vm.network :forwarded_port, guest: 4041,   host: 4041,  host_ip: "127.0.0.1"

  ## Superset 
  config.vm.network :forwarded_port, guest: 3088,   host: 3088,  host_ip: "127.0.0.1"

  ## hue
  config.vm.network :forwarded_port, guest: 8000,   host: 8000,  host_ip: "127.0.0.1"

end
