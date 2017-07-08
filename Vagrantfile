# coding: utf-8
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  # vagrant box list とかで出てくるやつ
  config.vm.box = "centos72"

  config.vm.hostname = "vagrant"

  # ホストのポート 8080 をvagrantの80につなげる
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # ipアドレス ipは適当に変更しておｋ
  # config.vm.network(:private_network, {:type=>"static", :ip=>"172.28.35.102"})
  config.vm.network :private_network, ip: "192.168.33.10"
  config.ssh.insert_key = false
  config.ssh.forward_agent = true

  # ホストとディレクトリを同期する例
  config.vm.synced_folder "./umagraph", "/home/vagrant/umagraph",  type:"rsync", create: true, mount_options: ["uid=vagrant,gid=vagrant"]
  config.vm.synced_folder "./ansible", "/home/vagrant/ansible",  type:"rsync", create: true, mount_options: ["uid=vagrant,gid=vagrant"]

  # ansibleの設定
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/provision.yml"
  end
end
