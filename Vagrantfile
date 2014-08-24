# -*- mode: ruby -*-
# vim: set ft=ruby :

# Sample vagrant box for docker testing
#
# @createdby mjl 10-aug-14

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box= "chef/centos-6.5"
  #config.vm.box_url= "https://vagrantcloud.com/chef/centos-6.5/version/1/provider/virtualbox.box"
  config.vm.provision "shell", inline: $script
  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024"]
  end
end

$script = <<SCRIPT
function execcmd() {
  echo "------------- executing: $@"
  "$@"
  RESULT=$?
  if [ $RESULT -ne 0 ]; then
    echo ">>>>  COMMAND FAILED [$@], aborting"
    exit $RESULT
  fi
}

#install docker -- from http://www.liquidweb.com/kb/how-to-install-docker-on-centos-6/
execcmd rpm -iUvh http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
#execcmd yum update -y
execcmd yum -y install docker-io
execcmd service docker start
execcmd chkconfig docker on

SCRIPT
