# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "fedora/27-cloud-base"

  config.vm.provision "shell" do |shell|
    shell.privileged = true
    shell.inline = <<-SHELL
    useradd dummy_user
    echo dummy_password | passwd dummy_user --stdin
    mkdir -p /home/dummy_user/.ssh
    chmod 'u=rwx,go=' /home/dummy_user/.ssh
    cp /vagrant/keys/dummy_key_10* /home/dummy_user/.ssh/
    chown -R dummy_user:dummy_user /home/dummy_user
    cp /vagrant/keys/dummy_key_10.pub /home/dummy_user/.ssh/authorized_keys
    chmod 'u=rw,go=' /home/dummy_user/.ssh/authorized_keys
    sed -i \
        -e 's/PermitRootLogin/#PermitRootLogin/g' \
        -e 's/#MaxAuthTries 6/MaxAuthTries 3/g' \
        -e 's/PasswordAuthentication yes/PasswordAuthentication no/g' \
        /etc/ssh/sshd_config
    systemctl restart sshd
    SHELL
  end
end
