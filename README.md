# vagrant-ansible テンプレート

## dependency

* Git
* Ansible

### Gitのインストール

`yun install git` とか `apt-get install git` とか

### Ansibleのインストール

Mac

```
$ brew install ansible
```

## 使い方

### 1, このリポジトリをcloneします

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
