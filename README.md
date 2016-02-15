# vagrant-ansible テンプレート

## dependency

* virtualbox
* vagrant
* Git
* Ansible

### Ubuntu

#### Virtualbox

/etc/apt/sources.list に以下を追加

```
# for vagrant
deb http://download.virtualbox.org/virtualbox/debian raring contrib
```

https://www.virtualbox.org/wiki/Linux_Downloads のDebian-based Linux distributins を参考に

```
$ wget https://www.virtualbox.org/download/oracle_vbox.asc
$ sudo apt-key add oracle_vbox.asc
OK
$ sudo apt-get update
$ sudo apt-get install virtualbox-5.0
```

#### Vagrant

https://www.vagrantup.com/downloads.html の deb ファイルを利用して

```
$ sudo apt-get install dpkg
$ wget https://dl.bintray.com/mitchellh/vagrant/vagrant_1.7.2_i686.deb
$ sudo dpkg --install vagrant_1.8.1_x86_64.deb
```

インストールされていることを確認する

```
$ vagrant --version
Vagrant 1.8.1
```

#### 参考ページ

* https://inexio.jp/20150707-944
* http://qiita.com/seizans/items/ef220c98fde6dbfbee32

#### Ansibleのインストール

```
$ sudo apt-get install ansible
```

#### vagrant 動作確認

http://www.vagrantbox.es/ から box を決める。今回は試しに Cent OS 7 を入れてみる

```
$ vagrant box add centos7 https://github.com/tommy-muehle/puppet-vagrant-boxes/releases/download/1.1.0/centos-7.0-x86_64.box
$ vagrant box list
centos7 (virtualbox, 0)
```

このリポジトリをクローンして、 `centos7` を設定。最小構成（ `ansible/provision.xml` の中身を全部コメントアウト）で vagrant up してみる。

```
$ vagrant up
$ vagrant ssh
# ssh接続できる
```

### Gitのインストール

`yun install git` とか `apt-get install git` とか

### Ansibleのインストール

Mac

```
$ brew install ansible
```

## 使い方

### 1, このリポジトリをcloneします

```
git clone https://github.com/yoshikyoto/vagrant-ansible.git my-vagrant
```

### 2. Vagrantfile をお好みに書き換えます

boxの名前とかネットワークの設定とかを書き換えます

### 3. playbook を適当に書き換えます

`ansible/provision.xml` をいい感じに編集して、使いたいミドルウェアだけ入れていきます

### 4. vagrantの起動とprovisioning

初回起動時は `vagrant_up` で自動的にprovisioningが走ると思います。

初回起動時以外で、vagrantの起動と同時にansibleを流す。

```
$ vagrant up --provision
```

起動しているvagrantにansibleを流す。

```
$ vagrant provision
```

__Failed to mount folders in Linux guest. と言われた場合__

```
Failed to mount folders in Linux guest. This is usually because
the "vboxsf" file system is not available. Please verify that
the guest additions are properly installed in the guest and
can work properly. The command attempted was:

mount -t vboxsf -o uid=`id -u vagrant`,gid=`getent group vagrant | cut -d: -f3` vagrant /vagrant
mount -t vboxsf -o uid=`id -u vagrant`,gid=`id -g vagrant` vagrant /vagrant

The error output from the last command was:

/sbin/mount.vboxsf: mounting failed with the error: No such device
```

boxを最新版にしてみてください。

## Tips

### Apache

* ホーム: `/usr/local/apache2`
* 設定: `/usr/local/apache2/conf/httpd.conf`
