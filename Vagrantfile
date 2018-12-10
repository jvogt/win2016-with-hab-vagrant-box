# -*- mode: ruby -*-
# vi: set ft=ruby :
$main_provisioner = <<-SCRIPT
iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
C:/ProgramData/chocolatey/choco install git -y --no-progress
C:/ProgramData/chocolatey/choco install GoogleChrome -y --no-progress
C:/ProgramData/chocolatey/choco install VisualStudioCode -y --no-progress
C:/ProgramData/chocolatey/choco install cmder -y --no-progress
New-NetFirewallRule -DisplayName \"Habitat TCP\" -Direction Inbound -Action Allow -Protocol TCP -LocalPort 9631,9638
New-NetFirewallRule -DisplayName \"Habitat UDP\" -Direction Inbound -Action Allow -Protocol UDP -LocalPort 9638
C:/ProgramData/chocolatey/choco install habitat -y --no-progress
#C:/ProgramData/chocolatey/choco install docker-for-windows --pre -y --no-progress
#C:/ProgramData/chocolatey/choco install docker -y --no-progress
C:/ProgramData/chocolatey/choco install powershell-core -y
Install-PackageProvider -Name NuGet -Force
Install-Module -Name DockerMsftProvider -Force
Install-Package -Name docker -ProviderName DockerMsftProvider -Force
SCRIPT

Vagrant.configure("2") do |config|
  #config.vm.box = "mwrock/Windows2016" # may not be updated - cant install containers feature
  config.vm.box = "chef/windows-server-2016-standard"
  config.vm.provider "virtualbox" do |v|
    v.gui = false
    v.linked_clone = true
    v.memory = 1024
    v.cpus = 2
  end
  config.vm.synced_folder ".", "/vagrant"
  config.vm.provision "shell", inline: "install-windowsfeature containers"
  config.vm.provision :reload
  config.vm.provision "shell", inline: $main_provisioner
  config.vm.provision :reload
  config.vm.provision "shell", inline: "docker pull habitat-docker-registry.bintray.io/win-studio"

end
