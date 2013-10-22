### Prerequisite 

1. Install [Oracle's virtual box](https://www.virtualbox.org/wiki/Downloads) for the host
1. Install latest [Vagrant software](http://downloads.vagrantup.com/)
1. Install Vagrant [Vagrant box images](http://www.vagrantbox.es/)

### Add base images (precise32, previse64, Windows 2008 Server R2 image)

1. Download images

		cd ~/Downloads
        wget -o win2k8rc.log -O win2k8rc.box "http://dl.dropboxusercontent.com/u/58604/vagrant/win2k8r2.box"
        wget -o precise64.log -O precise64.mbox  "http://files.vagrantup.com/precise64.box"
	    wget -o precise32.log -O precise32.mbox  "http://files.vagrantup.com/precise32.box"

1. Add the base image so multiple projects can share these images

        cd ~/Downloads
		vagrant box add win2k8r2 win2k8r2.box
		vagrant box add precise64 precise64.box
		vagrant box add precise64 precise32.box
		
    This will add virtual boxes image under ~/.vagrant.d directory.

### Create a Linux project

1. Create project directory, initialize vagrant configuration file

        mkdir ~/projects/<project-name>
        cd ~/projects/<project-name>
        vagrant init
        
1. Edit the *Vagrantfile* under the project directory to use the precise32 box 

        # Every Vagrant virtual environment requires a box to build off of.
        config.vm.box = "precise32"
        
1. Start up the vbox

        vagrant up

    FixMe: Only precise32 works on my Debian wheezy 64 bit host.

### Create a project for office365

1. Create project directory, initialize vagrant configuration file

        mkdir ~/projects/office365
        cd ~/projects/office365
      	vagrant init
      	
1. Edit the *Vagrantfile* under the project directory to use the Window Server box 

	    Vagrant.configure("2") do |config|
  		    config.vm.box = "win2k8r2"
		    vb.gui = true
	    end
	
1. Start the vobx

        vagrant up

1.  [Install Required Software](http://technet.microsoft.com/en-us/library/jj151815.aspx)

1. Use Device -> Add Guest Addons to install guest addions

1. Use Device -> Shared Folders to create a shared folder

1. Create [a share](http://www.virtualbox.org/manual/ch04.html#sf_mount_manual) so we can use the share from the host. 

    On host

	    cd ~/projects/office365
	    mkdir powershell
 
    On Guest:

		C:\net use x: \\vboxsvr\powershell
		C: Set-ExecutionPolicy Unrestricted
		
1. Create Powershell script with .ps1 with your favorite editor!

###  Debug

		VAGRANT_LOG=INFO vagrant up
		
### Destroy

		vagrant destroy
 
        
        
