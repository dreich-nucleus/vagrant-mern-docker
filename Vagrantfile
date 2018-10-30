# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  
  # BEGIN VMWARE SPECIFIC CONFIG
  # vmware fusion specific configuration to deal with pci slot changing in future
  config.vm.provider :vmare_desktop do |vmware|
    vmware.vmx["ethernet0.pcislotnumber"] = "33"
  end

  config.vm.provider "vmware_desktop" do |v|
    v.vmx["memsize"] = "8192"
    v.vmx["numvcpus"] = "4"
  end
  # END VMWARE SPECIFIC CONFIG

  # BEGIN VirtualBox SPECIFIC CONFIG
  config.vm.provider "virtualbox" do |v|
    v.memory = 8192
    v.cpus = 4
  end
  # END VirtualBox SPECIFIC CONFIG


  # use ubuntu 1604
  config.vm.box = "geerlingguy/ubuntu1604"

  # forward port 9000 for use by node
  config.vm.network "forwarded_port", guest: 9000, host: 9000

  # sync folder with rsync to one way sync source code in host to guest so we can use an editor running on the host.  Note that
  # rsync__args are the default EXCEPT for the --delete argument which would delete the node_modules directory
  config.vm.synced_folder "src", "/home/vagrant/src", type: "rsync", rsync__args: ["--verbose", "--archive", "-z", "--copy-links"],
    rsync__exclude: "node_modules/"

  # provision meteor
  config.vm.provision "shell", path: "bootstrap.sh"

end
