MySQLTuner-perl
====
[![Build Status - Master](https://travis-ci.org/major/MySQLTuner-perl.svg?branch=master)](https://travis-ci.org/major/MySQLTuner-perl)
[![Project Status](http://opensource.box.com/badges/active.svg)](http://opensource.box.com/badges)
[![Project Status](http://opensource.box.com/badges/maintenance.svg)](http://opensource.box.com/badges)
[![Average time to resolve an issue](http://isitmaintained.com/badge/resolution/major/MySQLTuner-perl.svg)](http://isitmaintained.com/project/major/MySQLTuner-perl "Average time to resolve an issue")
[![Percentage of open issues](http://isitmaintained.com/badge/open/major/MySQLTuner-perl.svg)](http://isitmaintained.com/project/major/MySQLTuner-perl "Percentage of issues still open")
[![GPL License](https://badges.frapsoft.com/os/gpl/gpl.png?v=103)](https://opensource.org/licenses/GPL-3.0/)

**MySQLTuner** is a script written in Perl that allows you to review a MySQL installation quickly and make adjustments to increase performance and stability.  The current configuration variables and status data is retrieved and presented in a brief format along with some basic performance suggestions.

**MySQLTuner** supports ~300 indicators for MySQL/MariaDB/Percona Server in this last version.

**MySQLTuner** is maintained and indicator collect is increasing week after week supporting a lot of configuration such as [Galera Cluster](http://galeracluster.com/), [TokuDB](https://www.percona.com/software/mysql-database/percona-tokudb), [Performance schema](https://github.com/mysql/mysql-sys), Linux OS metrics, [InnoDB](http://dev.mysql.com/doc/refman/5.7/en/innodb-storage-engine.html), [MyISAM](http://dev.mysql.com/doc/refman/5.7/en/myisam-storage-engine.html), [Aria](https://mariadb.com/kb/en/mariadb/aria/), ...

You can find more details on these indicators here:
[Indicators description](https://github.com/major/MySQLTuner-perl/blob/master/INTERNALS.md).


![MysqlTuner](https://github.com/major/MySQLTuner-perl/blob/master/mysqltuner.png)

MySQLTuner needs you:
===

**MySQLTuner** needs contributors for documentation, code and feedback..

* Please join us on issue track at [GitHub tracker](https://github.com/major/MySQLTuner-perl/issues).
* Contribution guide is available following [MySQLTuner contributing guide](https://github.com/major/MySQLTuner-perl/blob/master/CONTRIBUTING.md)
* Star **MySQLTuner project** at [MySQLTuner Git Hub Project](https://github.com/major/MySQLTuner-perl)
## Stargazers over time

[![Stargazers over time](https://starcharts.herokuapp.com/major/MySQLTuner-perl.svg)](https://starcharts.herokuapp.com/major/MySQLTuner-perl)

Compatibility
====
Test result are available here: [Travis CI/MySQLTuner-perl](https://travis-ci.org/major/MySQLTuner-perl)
* MySQL 8 (partial support, password checks don't work)
* MySQL 5.7 (full support)
* MySQL 5.6 (full support)
* MariaDB 10.3 (full support)
* MariaDB 10.2 (full support)
* MariaDB 10.1 (full support)
* MariaDB 10.0 (full support, 6 last month support)
* Percona Server 5.7 (full support)
* Percona Server 5.6 (full support)
* Percona XtraDB cluster (full support)
* MySQL 3.23, 4.0, 4.1, 5.0, 5.1, 5.5 (partial support - deprecated version)
* Perl 5.6 or later (with [perl-doc](http://search.cpan.org/~dapm/perl-5.14.4/pod/perldoc.pod) package)
* Unix/Linux based operating system (tested on Linux, BSD variants, and Solaris variants)
* Windows is not supported at this time (Help wanted !!!!!)
* Unrestricted read access to the MySQL server (OS root access recommended for MySQL < 5.1)
* CVE vulnerabilities detection support from [https://cve.mitre.org](https://cve.mitre.org)

***WARNING***
--
It is **extremely important** for you to fully understand each change
you make to a MySQL database server.  If you don't understand portions
of the script's output, or if you don't understand the recommendations,
**you should consult** a knowledgeable DBA or system administrator
that you trust.  **Always** test your changes on staging environments, and
always keep in mind that improvements in one area can **negatively affect**
MySQL in other areas.

**Seriously - please review the FAQ section below.**


Security recommendations
--

Hi directadmin user!
We detected that you run mysqltuner with da_admin's credentials taken from `/usr/local/directadmin/conf/my.cnf`, which might bring to a password discovery!
Read link for more details [Issue #289](https://github.com/major/MySQLTuner-perl/issues/289).

What MySQLTuner is checking exactly ?
--
All checks done by **MySQLTuner** are documented in [MySQLTuner Internals](https://github.com/major/MySQLTuner-perl/blob/master/INTERNALS.md) documentation.

Download/Installation
--

Choose one of these methods:

1) Script direct download (the simplest and shortest method):

```
wget http://mysqltuner.pl/ -O mysqltuner.pl
wget https://raw.githubusercontent.com/major/MySQLTuner-perl/master/basic_passwords.txt -O basic_passwords.txt
wget https://raw.githubusercontent.com/major/MySQLTuner-perl/master/vulnerabilities.csv -O vulnerabilities.csv
```

2) You can download the entire repository by using `git clone` or `git clone --depth 1 -b master` followed by the cloning URL above.

Optional Sysschema installation for MySQL 5.6
--

Sysschema is installed by default under MySQL 5.7 and MySQL 8 from Oracle.
By default, on MySQL 5.6/5.7/8, performance schema is enabled by default.
For previous 5.6 version, you can follow this command to create a new database sys containing very useful view on Performance schema:
	
	curl "https://codeload.github.com/mysql/mysql-sys/zip/master" > sysschema.zip
	# check zip file
	unzip -l sysschema.zip
	unzip sysschema.zip
	cd mysql-sys-master
	mysql -uroot -p < sys_56.sql 

Optional Performance schema and Sysschema installation for MariaDB 10.x
--

Sysschema is not installed by default under MariaDB 10.x.
By default, on MariaDB, performance schema is disabled by default. consider activating performance schema across your my.cnf configuration file:

	[mysqld]
	performance_schema = on

You can follow this command to create a new database sys containing very useful view on Performance schema:
	
	curl "https://codeload.github.com/good-dba/mariadb-sys/zip/master" > mariadb-sys.zip
	# check zip file
	unzip -l mariadb-sys.zip
	unzip mariadb-sys.zip
	cd mariadb-sys/
	mysql -u root -p < ./mariadb_sys_install.sql

Performance tips
--
Metadata statistic updates can impact strongly performance of database servers and MySQLTuner.
Be sure that innodb_stats_on_metadata is disabled.

	set global innodb_stats_on_metadata = 0; 

Specific usage
--

__Usage:__ Minimal usage locally

	perl mysqltuner.pl

Of course, you can add the execute bit (`chmod +x mysqltuner.pl`) so you can execute it without calling perl directly.

__Usage:__ Minimal usage remotely

	perl mysqltuner.pl --host targetDNS_IP --user admin_user --pass admin_password

__Usage:__ Enable maximum output information around MySQL/MariaDb without debugging

	perl mysqltuner.pl --verbose
	perl mysqltuner.pl --buffers --dbstat --idxstat --sysstat --pfstat --tbstat


__Usage:__ Enable CVE vulnerabilities check for your MariaDB or MySQL version

	perl mysqltuner.pl --cvefile=vulnerabilities.csv

__Usage:__ Write your result in a file with information displayed  

	perl mysqltuner.pl --outputfile /tmp/result_mysqltuner.txt

__Usage:__ Write your result in a file **without outputting information**

	perl mysqltuner.pl --silent --outputfile /tmp/result_mysqltuner.txt

__Usage:__ Using template model to customize your reporting file based on [Text::Template](https://metacpan.org/pod/Text::Template) syntax.

 	perl mysqltuner.pl --silent --reportfile /tmp/result_mysqltuner.txt --template=/tmp/mymodel.tmpl

__Usage:__ Enable debugging information

	perl mysqltuner.pl --debug

FAQ
--

**Question: Will MySQLTuner fix my slow MySQL server?**

**No.**  MySQLTuner is a read only script.  It won't write to any configuration files, change the status of any daemons, or call your mother to wish her a happy birthday.  It will give you an overview of your server's performance and make some basic recommendations for improvements that you can make after it completes.  *Make sure you read the warning above prior to following any recommendations.*

**Question: Can I fire my DBA now?**

**MySQLTuner will not replace your DBA in any form or fashion.**  If your DBA constantly takes your parking spot and steals your lunch from the fridge, then you may want to consider it - but that's your call.

**Question: Why does MySQLTuner keep asking me the login credentials for MySQL over and over?**

The script will try its best to log in via any means possible.  It will check for ~/.my.cnf files, Plesk password files, and empty password root logins.  If none of those are available, then you'll be prompted for a password.  If you'd like the script to run in an automated fashion without user intervention, then create a .my.cnf file in your home directory which contains:

	[client]
	user=someusername
	pass=thatuserspassword

Once you create it, make sure it's owned by your user and the mode on the file is 0600.  This should prevent the prying eyes from getting your database login credentials under normal conditions.  If a [T-1000 shows up in a LAPD uniform](https://en.wikipedia.org/wiki/T-1000) and demands your database credentials, you won't have much of an option.

**Question: Is there another way to secure credentials on latest MySQL and MariaDB distributions ?**

You could use mysql_config_editor utilities.
~~~bash
	$ mysql_config_editor set --login-path=client --user=someusername --password --host=localhost
	Enter password: ********
~~~
After which, `~/.mylogin.cnf` will be created with the appropriate access.

To get information about stored credentials, use the following command:

	$mysql_config_editor print
	[client]
	user = someusername
	password = *****
	host = localhost

**Question: What's minimum privileges needed by a specific mysqltuner user in database ?**

        mysql>GRANT SELECT, PROCESS,EXECUTE, REPLICATION CLIENT,SHOW DATABASES,SHOW VIEW ON *.* FOR 'mysqltuner'@'localhost' identified by pwd1234;

**Question: It's not working on my OS! What gives?!**

These kinds of things are bound to happen.  Here are the details I need from you in order to research the problem thoroughly:

* OS and OS version
* Architecture (x86, x86_64, IA64, Commodore 64)
* Exact MySQL version
* Where you obtained your MySQL version (OS package, source, etc)
* The full text of the error
* A copy of SHOW VARIABLES and SHOW GLOBAL STATUS output (if possible)

**Question: How to perform CVE vulnerability checks?**

* Download vulnerabilities.csv from this repository.
* use option --cvefile to perform CVE checks

**Question: How to use mysqltuner from a remote host?**
Thanks to  [@rolandomysqldba](http://dba.stackexchange.com/users/877/rolandomysqldba)

* You will still have to connect like a mysql client:

Connection and Authentication

	--host <hostname> Connect to a remote host to perform tests (default: localhost)
	--socket <socket> Use a different socket for a local connection
	--port <port>     Port to use for connection (default: 3306)
	--user <username> Username to use for authentication
	--pass <password> Password to use for authentication
	--defaults-file <path> defaults file for credentials

Since you are using a remote host, use parameters to supply values from the OS

	--forcemem <size>  Amount of RAM installed in megabytes
	--forceswap <size> Amount of swap memory configured in megabytes

* You may have to contact your remote SysAdmin to ask how much RAM and swap you have

If the database has too many tables, or very large table, use this:

	--skipsize           Don't enumerate tables and their types/sizes (default: on)
	                     (Recommended for servers with many tables)

**Question: Can I install this project using homebrew on Apple Macintosh?**

Yes! `brew install mysqltuner` can be used to install this application using [homebrew](https://brew.sh/) on Apple Macintosh.

MySQLTuner and Vagrant
--
**MySQLTuner** contains following Vagrant configurations:
* Fedora Core 23 / MariaDB 10.0
* Fedora Core 23 / MariaDB 10.1
* Fedora Core 23 / MySQL 5.6
* Fedora Core 23 / MySQL 5.7

**Vagrant File** are stored in Vagrant subdirectory.
* Follow this 2 steps after vagrant installation:
* Rename VagrantFile_for_Mxxx into Vagrantfile
* vagrant up

**MySQLTuner** contains a Vagrant configurations for test purpose and development
* Install VirtualBox and Vagrant
	* https://www.virtualbox.org/wiki/Downloads
	* https://www.vagrantup.com/downloads.html
* Clone repository
 	* git clone https://github.com/major/MySQLTuner-perl.git
* Install Vagrant plugins vagrant-hostmanager and  vagrant-vbguest
	* vagrant plugin install vagrant-hostmanager
	* vagrant plugin install vagrant-vbguest
* Add Fedora Core 23 box for official Fedora Download Website
	* vagrant box add --name fc23 https://download.fedoraproject.org/pub/fedora/linux/releases/23/Cloud/x86_64/Images/Fedora-Cloud-Base-Vagrant-23-20151030.x86_64.vagrant-virtualbox.box
* Create a data directory
	* mkdir data
* Rename Vagrantfile_MariaDB10.0 into Vagrantfile
	* cp MySQLTuner-perl/Vagrant/Vagrantfile_for_MariaDB10.0 Vagrantfile
* Start vagrant
	* vagrant up

MySQLTuner needs you
--
**MySQLTuner** needs contributors for documentation, code and feedback..

* Please join us on issue track at [GitHub tracker](https://github.com/major/MySQLTuner-perl/issues).
* Contribution guide is available following [MySQLTuner contributing guide](https://github.com/major/MySQLTuner-perl/blob/master/CONTRIBUTING.md)
* Star **MySQLTuner project** at [MySQLTuner Git Hub Project](https://github.com/major/MySQLTuner-perl)
