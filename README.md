# Using Veewee on OSX 10.9 to build a Debian VM for use with Vagrant  

The Veewee instructions can be found [here](https://github.com/jedi4ever/veewee/blob/master/doc/basics.md).

This tutorial focuses on running Veewee on OSX 10.9 to build a Debian VM for use with Vagrant.

## Install rvm using homebrew
http://www.moncefbelyamani.com/how-to-install-xcode-homebrew-git-rvm-ruby-on-mac/

		brew install rvm
		curl -L https://get.rvm.io | bash -s stable --rails --autolibs=enable
		source /Users/jasondarwin/.rvm/scripts/rvm
		rvm requirements
		brew tap --repair
		brew doctor
		brew unlink libxml2

## Install Ruby using rvm and homebrew

		rvm requirements
		rvm install ruby-2.0.0-p353
		brew link libyaml
		brew link --overwrite --dry-run libyaml
		brew link --overwrite libyaml
		rvm install ruby-2.0.0-p353
		rm /Library/Caches/Homebrew/openssl-1.0.1e.tar.gz
		brew install openssl
		rvm install ruby-2.0.0-p353

## Install Veewee

		git clone https://github.com/jedi4ever/veewee.git
		cd veewee/
		sudo gem install bundler
		sudo bundle install

## Use Veewee to build our VM

		bundle exec veewee
		veewee
		veewee vbox templates
		veewee vbox define debian-7.2.0-i386-netboot Debian-7.2.0-i386-netboot
		veewee vbox build 'debian-7.2.0-i386-netboot' --workdir=/Users/jasondarwin/workspace/veewee
		ls -la ~/VirtualBox\ VMs/

## Use Veewee to export our built VM to Virtual Box / Vagrant format

		veewee vbox export debian-7.2.0-i386-netboot

## Import into Vagrant

		# To import it into vagrant type:
		vagrant box add 'debian-7.2.0-i386-netboot' '/Users/jasondarwin/workspace/veewee/debian-7.2.0-i386-netboot.box'

		# To use it:
		vagrant init 'debian-7.2.0-i386-netboot'
		vagrant up
		vagrant ssh