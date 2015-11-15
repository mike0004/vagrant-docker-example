# Sample vagrant box for docker testing
#
# @createdby mjl 14-nov-2015

VAGRANTFILE_API_VERSION = 

Vagrant.configure("2") do |config|
  config.vm.box= "centos/7"
  config.vm.provision "shell", inline: $script
  config.vm.provider "virtualbox" do |vb|
    vb.memory="2048"
    vb.cpus="2"
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

# install docker on centos 7: http://docs.docker.com/v1.8/installation/centos/
# this is the cheapo omnibus way but it should work

execcmd yum update -y
execcmd curl -sSL https://get.docker.com/ | sh
execcmd service docker start
execcmd docker run hello-world

SCRIPT
