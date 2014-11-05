# What is this spec?

Import kyototycoon.spec of https://github.com/kyohsuke/srpms/blob/master/kyototycoon-0.9.56-1.src.rpm

# Example to build SRPM and RPM

You need to install [VirtualBox](https://www.virtualbox.org/) and [Vagrant](http://www.vagrantup.com/).

```
$ vagrant up
$ vagrant ssh
$ mkdir -p ~/rpmbuild/{BUILD,BUILDROOT,RPMS,SOURCES,SPECS,SRPMS}
$ (cd ~/rpmbuild/SOURCES && curl -LO http://fallabs.com/kyototycoon/pkg/kyototycoon-0.9.56.tar.gz)
$ cp /vagrant/kyototycoon.spec ~/rpmbuild/SPECS
$ sudo yum update -y
$ sudo yum install -y rpm-build
$ rpmbuild -ba ~/rpmbuild/SPECS/kyototycoon.spec
エラー: ビルド依存性の失敗:
        kernel-devel >= 2.6.17 は kyototycoon-0.9.56-1.x86_64 に必要とされています
        kyotocabinet-devel は kyototycoon-0.9.56-1.x86_64 に必要とされています
        gcc-c++ は kyototycoon-0.9.56-1.x86_64 に必要とされています
        zlib-devel は kyototycoon-0.9.56-1.x86_64 に必要とされています
        autoconf は kyototycoon-0.9.56-1.x86_64 に必要とされています
        automake は kyototycoon-0.9.56-1.x86_64 に必要とされています
$ curl -LO https://github.com/feedforce/kyotocabinet-rpm/releases/download/1.2.76/kyotocabinet-devel-1.2.76-1.x86_64.rpm
$ sudo rpm -ivh kyotocabinet-devel-1.2.76-1.x86_64.rpm
エラー: 依存性の欠如:
        kyotocabinet = 1.2.76-1 は kyotocabinet-devel-1.2.76-1.x86_64 に必要とされています
        libkyotocabinet.so.16()(64bit) は kyotocabinet-devel-1.2.76-1.x86_64 に必要とされています
$ curl -LO https://github.com/feedforce/kyotocabinet-rpm/releases/download/1.2.76/kyotocabinet-1.2.76-1.x86_64.rpm
$ sudo rpm -ivh kyotocabinet-1.2.76-1.x86_64.rpm
$ sudo rpm -ivh kyotocabinet-devel-1.2.76-1.x86_64.rpm
$ sudo yum install -y kernel-devel gcc-c++ zlib-devel autoconf automake
$ rpmbuild -ba ~/rpmbuild/SPECS/kyototycoon.spec
(snip)
書き込み完了: /home/vagrant/rpmbuild/SRPMS/kyototycoon-0.9.56-1.src.rpm
書き込み完了: /home/vagrant/rpmbuild/RPMS/x86_64/kyototycoon-0.9.56-1.x86_64.rpm
書き込み完了: /home/vagrant/rpmbuild/RPMS/x86_64/kyototycoon-devel-0.9.56-1.x86_64.rpm
```

## How to build RPM from SRPM

```
$ vagrant up
$ vagrant ssh
$ sudo yum update -y
$ sudo yum install -y rpm-build
$ curl -LO https://github.com/feedforce/kyototycoon-rpm/releases/download/0.9.56/kyototycoon-0.9.56-1.src.rpm
$ rpmbuild --rebuild kyototycoon-0.9.56-1.src.rpm
kyototycoon-0.9.56-1.src.rpm をインストール中です。
エラー: ビルド依存性の失敗:
        kernel-devel >= 2.6.17 は kyototycoon-0.9.56-1.x86_64 に必要とされています
        kyotocabinet-devel は kyototycoon-0.9.56-1.x86_64 に必要とされています
        gcc-c++ は kyototycoon-0.9.56-1.x86_64 に必要とされています
        zlib-devel は kyototycoon-0.9.56-1.x86_64 に必要とされています
        autoconf は kyototycoon-0.9.56-1.x86_64 に必要とされています
        automake は kyototycoon-0.9.56-1.x86_64 に必要とされています
$ curl -LO https://github.com/feedforce/kyotocabinet-rpm/releases/download/1.2.76/kyotocabinet-devel-1.2.76-1.x86_64.rpm
$ sudo rpm -ivh kyotocabinet-devel-1.2.76-1.x86_64.rpm
エラー: 依存性の欠如:
        kyotocabinet = 1.2.76-1 は kyotocabinet-devel-1.2.76-1.x86_64 に必要とされています
        libkyotocabinet.so.16()(64bit) は kyotocabinet-devel-1.2.76-1.x86_64 に必要とされています
$ curl -LO https://github.com/feedforce/kyotocabinet-rpm/releases/download/1.2.76/kyotocabinet-1.2.76-1.x86_64.rpm
$ sudo rpm -ivh kyotocabinet-1.2.76-1.x86_64.rpm
$ sudo rpm -ivh kyotocabinet-devel-1.2.76-1.x86_64.rpm
$ sudo yum install -y kernel-devel gcc-c++ zlib-devel autoconf automake
$ rpmbuild --rebuild kyototycoon-0.9.56-1.src.rpm
(snip)
書き込み完了: /home/vagrant/rpmbuild/RPMS/x86_64/kyototycoon-0.9.56-1.x86_64.rpm
書き込み完了: /home/vagrant/rpmbuild/RPMS/x86_64/kyototycoon-devel-0.9.56-1.x86_64.rpm
```
