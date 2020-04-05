VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "hashicorp/bionic64"

  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--usb", "on"]
    vb.customize ['usbfilter', 'add', '0', '--target', :id, '--name', 'NVidia', '--vendorid', '0x0955']
  end

  config.vm.provision "dependencies", type: "shell" do |s|
    s.inline = <<-SCRIPT
      sudo apt-get update
      sudo apt-get install -y libgtk-3-0 libx11-xcb1 libxss1 libnss3 xvfb
      sudo apt-get install -y /vagrant/sdkmanager*
    SCRIPT
  end

  config.vm.provision "install", type: "shell", privileged: false, run: "never" do |s|
    s.inline = <<-SCRIPT
      xvfb-run sdkmanager --cli install --responsefile $1 --host --flash skip --exitonfinish || true
    SCRIPT
    s.args = "/vagrant/sdkm_responsefile.ini"
  end
end
