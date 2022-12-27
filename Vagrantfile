Vagrant.configure("2") do |config| 
  # box
  config.vm.box = "bento/ubuntu-20.04"
  # ポートフォワーディング
  config.vm.network "forwarded_port", guest: 80, host: 80
  config.vm.network "forwarded_port", guest: 443, host: 443
  # メモリ/CPU
  config.vm.provider "virtualbox" do |vb|
    vb.memory = 4096
    vb.cpus = 2
  end

  # config.vm.synced_folder "C:/develop2/test", "/usr/local/html"
  
  # dockerとdocker-compose(v2.6.0)のインストール
  $get_compose = <<-'EOF'
  sudo apt-get update
  sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    postgresql-client \
    gnupg \
    lsb-release

  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
  echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  sudo apt update
  sudo apt -y install docker-ce docker-ce-cli containerd.io
  sudo curl -L https://github.com/docker/compose/releases/download/v2.6.0/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
  sudo chmod +x /usr/local/bin/docker-compose
  EOF
  config.vm.provision "shell", inline: $get_compose
end
