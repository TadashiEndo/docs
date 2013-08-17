# install openstack for centos on virturlbox
>
eth1の追加  
yum install -y ntp  
yum lock を消すとき  
rm -f /var/run/yum.pid  
yum のキャッシュを消してダウンロードを早くする  
/var/cache/yum/x86_64/6/timedhosts.txt  
yum -y install wget  
wget http://repos.fedorapeople.org/repos/openstack/openstack-grizzly/fedora-openstack-grizzly.repo  
mv fedora-openstack-grizzly.repo /etc/yum.repos.d/  
yum install mysql mysql-server MySQL-python  
sed -i 's/127.0.0.1/0.0.0.0/g' /etc/my.cnf  
意味ない  
/etc/init.d/mysql start
chkconfig mysqld on  
```
mysql -u root -p <<EOF
CREATE DATABASE nova;
GRANT ALL PRIVILEGES ON nova.* TO 'nova'@'localhost' \
IDENTIFIED BY 'password';
CREATE DATABASE cinder;
GRANT ALL PRIVILEGES ON cinder.* TO 'cinder'@'localhost' \
IDENTIFIED BY 'password';
CREATE DATABASE glance;
GRANT ALL PRIVILEGES ON glance.* TO 'glance'@'localhost' \
IDENTIFIED BY 'password';
CREATE DATABASE keystone;
GRANT ALL PRIVILEGES ON keystone.* TO 'keystone'@'localhost' \
IDENTIFIED BY 'password';
CREATE DATABASE quantum;
GRANT ALL PRIVILEGES ON quantum.* TO 'quantum'@'localhost' \
IDENTIFIED BY 'password';
FLUSH PRIVILEGES;
EOF
```
空白で　Enter
yum -y install qpid-cpp-server
echo auth=1 >> /etc/qpidd.conf
chkconfig qpidd on
エラー
auth=1 をコメントあうと


