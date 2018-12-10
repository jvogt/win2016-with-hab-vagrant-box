# Windows 2016 Server with Habitat environment baked in

This project is used to build a custom vagrant box from a base Windows 2016 image.

Requirements:
- vagrant
- virtualbox
- access to chef/windows-server-2016-standard box (only available to chef employees)

Steps:

1. Run `vagrant up`.  This will build a base Windows 2016 server and install container feature + docker + habitat.
2. `vagrant rdp` into the new VM to perform any additional customizations that you want to save in the resulting box.
3. Run `vagrant package --vagrantfile Vagrant-repackage`.  This will create a new vagrant box from a snapshot of the running box.
4. Run `vagrant box add package.box --name win2016-with-hab`

To run the box, copy `Vagrantfile-example` to a new directory, name it `Vagrantfile`, and then run `vagrant up`
