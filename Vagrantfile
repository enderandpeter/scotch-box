# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

    config.vm.box = "scotch/box"
    config.vm.network "private_network", type: "dhcp"
    config.vm.hostname = "scotchbox"
    config.vm.synced_folder "www", "/var/www", :nfs => { :mount_options => ["dmode=775", "fmode=664"] }
    config.vm.provision "file", source: "conf.d/spytecinc.conf", destination: "/tmp/spytecinc.conf"
    config.vm.provision "shell", privileged: true, inline: <<-SHELL 
mkdir --parents /home/vagrant/bin && \
cd /tmp && \
wget https://files.magerun.net/n98-magerun.phar && \
chmod +x /tmp/n98-magerun.phar && \
chown -R vagrant: /home/vagrant/bin && \
mv /tmp/n98-magerun.phar /home/vagrant/bin/n98-magerun && \
cp /tmp/spytecinc.conf /etc/apache2/sites-available/spytecinc.conf && \
a2ensite spytecinc && \
apachectl restart
    SHELL
    # Optional NFS. Make sure to remove other synced_folder line too
    #config.vm.synced_folder ".", "/var/www", :nfs => { :mount_options => ["dmode=777","fmode=666"] }

end
