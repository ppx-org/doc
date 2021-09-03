
centos7.9

https://www.postgresql.org/docs/13/index.html

# Packages and Installers
https://www.postgresql.org/download/

# Install the repository RPM:
sudo yum install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm

# Install PostgreSQL:
sudo yum install -y postgresql13-server

# Optionally initialize the database and enable automatic start:
sudo service postgresql-13 initdb 改成 /usr/pgsql-13/bin/postgresql-13-setup initdb
sudo chkconfig postgresql-13 on
sudo service postgresql-13 start

///////////////////////////////////////
配置监听和访问控制

echo "listen_addresses = '*'"  >> /var/lib/pgsql/13/data/postgresql.conf
echo "host all all all md5"  >> /var/lib/pgsql/13/data/pg_hba.conf

local   all             all                                     peer
改local   all             all                                     md5

sudo service postgresql-13 restart


管理配置>>>>>
# 重新设置postgres管理员密码
su - postgres
psql -U postgres
alter user postgres with password '#postgres13.4#';

# 创建普通用户和数据库，并退出
create user devuser with password '#devuser54321#';
create database devdb owner devuser encoding = 'UTF8';
\q

# test
psql -U devuser --password devdb
create table test(sid int, mm varchar(12));
insert into test values(1, 'aaa');
select * from test;
\q





















