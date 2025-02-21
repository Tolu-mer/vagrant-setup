Vagrant.configure("2") do |config|
  # Set Ubuntu as the base box
  config.vm.box = "ubuntu/bionic64"
  config.vm.box_version = "20191107.0.0"

  # Configure VM resources
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"  # Increased RAM for better performance
    vb.cpus = "2"
  end

  Vagrant.configure("2") do |config|
    config.vm.box = "debian/jessie64"
    config.vm.box_version = "8.11.1"
  end
 Vagrant.configure("2") do |config|
   config.vm.box = "centos/7"
   config.vm.box_version = "2004.01"
 end
  # Configure networking
  config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
  config.vm.network "public_network", ip: "192.168.33.10"

  # Provision the VM
  config.vm.provision "shell", inline: <<-SHELL
    # Update package lists
    sudo apt-get update

    # Install Nginx
    sudo apt-get install -y nginx
    sudo systemctl enable nginx
    sudo systemctl start nginx

    # Install Node.js (LTS version)
    curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
    sudo apt-get install -y nodejs

    # Install PostgreSQL
    sudo apt-get install -y postgresql postgresql-contrib

    # Set up PostgreSQL (create a user and database)
    sudo -u postgres psql -c "CREATE USER vagrant WITH PASSWORD 'vagrant';"
    sudo -u postgres psql -c "ALTER USER vagrant CREATEDB;"
    sudo -u postgres psql -c "CREATE DATABASE vagrantdb OWNER vagrant;"
  SHELL
end
