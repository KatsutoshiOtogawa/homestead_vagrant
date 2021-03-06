# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "laravel/homestead"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder "../projects", "/home/vagrant/projects"
  # プロジェクトの内容以外のファイル共有に使ってください。
  config.vm.synced_folder "../data", "/home/vagrant/data"
  
  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
      vb.memory = "4096"
  end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # homestedデフォルトのバージョンでそれぞれのパッケージが欲しいなら下記をコメントアウトしてください。
  config.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get -y upgrade

      # osが管理しているnpmだとちょっと古いので、バージョンアップ。
      npm install -g npm

      # docker 環境/開発確認用 いらないなら下記をコメントアウトしてください。
      # https://docs.docker.com/engine/install/ubuntu/
      apt-get -y install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
      curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
      apt-key fingerprint 0EBFCD88
      add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
      apt-get update && apt-get -y install docker-ce docker-ce-cli containerd.io

      # docker-compose 環境/開発確認用いらないなら下記をコメントアウトしてください。
      # https://docs.docker.com/compose/install/
      curl -L "https://github.com/docker/compose/releases/download/1.25.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
      chmod +x /usr/local/bin/docker-compose

      # gcp開発用　いらないなら下記をコメントアウトしてください。
      # cloud sdk install 右のページをみること https://cloud.google.com/sdk/docs/downloads-apt-get?hl=ja
      echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
      apt-get install apt-transport-https ca-certificates gnupg
      curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key --keyring /usr/share/keyrings/cloud.google.gpg add -
      apt-get update && apt-get -y install google-cloud-sdk
      # 必要に応じてcloud sdk追加のコンポーネントもインストールしてください。

      # aws開発用　いらないなら下記をコメントアウトしてください。
      # awscli install 右のページを参考に https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/install-linux.html
      apt -y install python3-pip
      pip3 install awscli --upgrade --user

  SHELL
end
