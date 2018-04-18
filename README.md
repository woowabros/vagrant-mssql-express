# vagrant-mssql-express

A Windows 2012 Server with SQL Server Express 2012 powered by Vagrant.

## 
이 리포지토리는 [mince27/vagrant-mssql-express](https://github.com/mince27/vagrant-mssql-express) 에서 Fork 한 것입니다.

### 설치
* [Vagrant](https://www.vagrantup.com/) 를 먼저 설치합니다.
* 설치 과정에서 `http://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x64/SQLEXPRWT_x64_ENU.exe`를 미리 다운받는 것이 좋습니다. wget이 없다면 다른 방법으로 다운받아 두세요.

```
git clone git@github.com:woowabros/vagrant-mssql-express.git
cd vagrant-mssql-express
wget http://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x64/SQLEXPRWT_x64_ENU.exe
vagrant up
```

### 접속 계정정보
* localhost:1443
* username: `sa`
* password: `password12!`

### CPU/Memory 조정
원한다면 `Vagrantfile'에서 cpus, memory 값을 원하는 것으로 조정가능하다.
```
'--memory', 2048,
'--cpus', 2
```

##

This repo was forked from [here](https://github.com/fgrehm/vagrant-mssql-express).  It was updated to support Sql Server Express 2012 on Windows Server 2012

## Requirements

* Vagrant 1.6+ (tested on 1.6.3)
* VirtualBox 4.3+ (tested on 4.3.16 on an Ubuntu host)
* Around `12GB` of disk space (`3GB` for base box + `~9GB` for the VM)

## Base box information

* Configured with 2 CPU and 2 GB memory by default.
* No updates or services packs applied
* The box is not activated. It has been created for testing and evaluation
  purposes only. Use of this machine for greater than 30 days will require a
  full license either via MSDN or your local Microsoft Reseller.
* The box has been created with [packer.io](http://www.packer.io/) using the
  templates made available [here](https://github.com/opentable/packer-images).

More information can be found on the [box page at Vagrant Cloud](https://atlas.hashicorp.com/opentable/boxes/win-2012r2-standard-amd64-nocm).

## Usage

```sh
git clone https://github.com/kwon37xi/vagrant-mssql-express.git
cd vagrant-mssql-express
wget 'http://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x64/SQLEXPRWT_x64_ENU.exe'
vagrant up
```
Get a coffee as it will take a while for it to finish provisioning.  The first time it has to download the vagrant box and sql server express.


### Connecting to the SQL Server instance that runs inside the VM

* IP / Host: `192.168.50.4
 * The ip will be the private_network value defined in `Vagrantfile`
 * Port Forwarding이 돼 있으므로 localhost:1433 으로 접속 가능
* Username: `sa`
* Password: `password12!'
 * To change this modify the value in `install-sql-server.cmd`

If you are using Rails you will need the following gems
```
gem 'tiny_tds'
gem 'activerecord-sqlserver-adapter', '~> 4.2.0'
```

This is what you'll have in your `database.yml`:

```yaml
development:
  adapter: sqlserver
  database: <YOUR DB>
  host: 192.168.50.4 # Should match the private_network in Vagrantfile
  username: sa
  password: 'password12!'
```

_More information on https://github.com/rails-sqlserver/activerecord-sqlserver-adapter/wiki/Using-TinyTDS_

An example [Sinatra](http://www.sinatrarb.com) app can be found on [sinatra-app](sinatra-app).

### Connecting to the VM using [Remote Desktop](https://en.wikipedia.org/wiki/Remote_Desktop_Protocol) connections

If you need to perform administrative tasks like importing a DB dump or creating
new databases, you can use the [`vagrant rdp` command](http://docs.vagrantup.com/v2/cli/rdp.html)
and log in with the `vagrant` user and password.

For the `vagrant rdp` command to work on Ubuntu, you'll need to `apt-get install rdesktop`
first.

On Macs, you will need [Microsoft Remote Desktop](https://itunes.apple.com/en/app/microsoft-remote-desktop/id715768417) from the Mac App Store.

* Username: vagrant
* Password: vagrant

## More information

If you want to know more about how the provisioning process work, check out
[this blog post](http://helabs.com.br/blog/2014/09/19/mssql-on-vagrant/)

## Sponsor

This project was made possible thanks to [HE:labs](http://helabs.com.br/en)

## Resources

Here's some links I collected along the way while building this:

* http://msdn.microsoft.com/en-us/library/ms144259%28v=SQL.100%29.aspx
* http://technet.microsoft.com/en-us/library/ee176858.aspx
* http://iqbalnaved.wordpress.com/2013/09/28/configuration-for-connecting-to-mssql-server-2008-on-virtualbox-guestos-from-ubuntu-12-04-hostos-using-pyodbc-3-0-8/
* http://technet.microsoft.com/en-us/library/dd206997(v=sql.105).aspx
* http://sirsql.net/blog/2011/6/21/set-the-sql-tcpip-port-with-powershell.html
