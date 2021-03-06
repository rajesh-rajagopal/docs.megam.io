---
title: Vertice
order: 1
---

{% include install_bulb.md %}

At the start, install OpenJDK8 and cassandra for which the following are needed.

### Supported Platforms

| Operating System                        | Status                                                |
|:-------------------------------------- :| :---------------------------------------------------- |
| Ubuntu 14.04, 16.04, Debian 8.5         | Well tested                                           |
| CentOS 7.2                              | Well tested


---

#### Ubuntu 14.04

##### OpenJDK8

~~~bash

$ sudo apt-add-repository -y ppa:openjdk-r/ppa

$ sudo apt-get -y update

$ sudo apt-get -y install openjdk-8-jdk

~~~

##### Ruby2.3

~~~bash

$ sudo apt-add-repository ppa:brightbox/ruby-ng

$ sudo apt-get -y update

$ sudo apt-get -y install ruby2.3 ruby2.3-dev

~~~

##### Ubuntu 16.04

~~~bash

$ sudo apt-get install openjdk-8-jre-headless

~~~  

##### Debian Jessie

~~~bash

$ echo "deb http://http.debian.net/debian jessie-backports main" > /etc/apt/sources.list

$ sudo apt-get update

$ sudo apt-get install openjdk-8-jre-headless

$ sudo apt-get install openjdk-8-jdk

$ sudo /usr/sbin/update-java-alternatives -s java-1.8.0-openjdk-amd64

~~~    

##### CentOS 7.2

##### OpenJDK8

~~~bash

$ wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u45-b14/jdk-8u45-linux-x64.rpm"

$ rpm -ivh jdk-8u45-linux-x64.rpm

~~~  

#### Cassandra 3.9

Install cassandra 3.9 by following the link for your operating system.


| Operating System             | Link                                                                                        |
|:--------------------------- :| :------------------------------------------------------------------------------------------ |
| Ubuntu 14.04/16.04/Debian 8.5|[Ubuntu/Debian](http://docs.datastax.com/en/cassandra/3.x/cassandra/install/installDeb.html){: target="_blank"} |
| CentOS 7.2                   |[CentOS](http://docs.datastax.com/en/cassandra/3.x/cassandra/install/installRHEL.html){: target="_blank"}       |
| Using tarball                |[All Linux using tarball](http://docs.datastax.com/en/cassandra/3.x/cassandra/install/installTarball.html){: target="_blank"}                                    |

##### Ubuntu 14.04

In case you find issues in installing cassandra 3.9 in *Ubuntu 14.04*, follow the instructions given below:

~~~bash

$ sudo echo "deb http://debian.datastax.com/datastax-ddc 3.9 main" | sudo tee -a /etc/apt/sources.list.d/cassandra.sources.list

$ sudo curl -L https://debian.datastax.com/debian/repo_key | sudo apt-key add -

$ sudo apt-get update

$ sudo apt-get install datastax-ddc

~~~

Restart the cassandra (in all operating systems)

~~~bash

$ service cassandra restart

~~~

Lets focus on update [Vertice](http://docs.megam.io/configuration/vertice/#import-vertice-keyspace) Keyspace & enable password authentication.

---

### Install OpenSource MegamVertice

#### Ubuntu 14.04 Version 1.5.2

~~~bash

  sudo apt-add-repository "deb [arch=amd64] http://get.megam.io/repo/1.5.2/ubuntu/14.04/testing trusty testing"

  sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 9B46B611

  sudo apt-get update

  sudo apt-get install verticenilavu verticegateway nsqd vertice verticevnc

~~~

Lets focus on Configure [Vertice](http://docs.megam.io/configuration/vertice/) Packages.

~~~

To start MegamVertice then

~~~bash

  sudo start nsqd

  sudo start nsqadmin

  sudo start nsqlookupd

  sudo start verticegateway

  sudo start verticevnc

  sudo start vertice

  sudo sv start nginx

  sudo sv start unicorn

~~~

To stop MegamVertice then

~~~bash

  sudo stop nsqd

  sudo stop nsqadmin

  sudo stop nsqlookupd

  sudo stop verticegateway

  sudo stop verticevnc

  sudo stop vertice

  sudo sv stop nginx

  sudo sv stop unicorn

~~~

#### Ubuntu 16.04/Debian Jessie Version 1.5.2

~~~bash

  sudo apt-add-repository "deb [arch=amd64] https://get.megam.io/repo/1.5.2/ubuntu/16.04/testing xenial testing"

  sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 9B46B611

  sudo apt-get update

  sudo apt-get install verticenilavu verticegateway nsqd vertice verticevnc

~~~

Lets focus on Configure [Vertice](http://docs.megam.io/configuration/vertice/) Packages.

~~~

To start MegamVertice

~~~bash

  sudo systemctl start nsqd

  sudo systemctl start nsqadmin

  sudo systemctl start nsqlookupd

  sudo systemctl start verticegateway

  sudo systemctl start verticevnc

  sudo systemctl start vertice

  sudo sv start nginx

  sudo sv start unicorn

~~~

To stop MegamVertice

~~~bash

  sudo systemctl stop nsqd

  sudo systemctl stop nsqadmin

  sudo systemctl stop nsqlookupd

  sudo systemctl stop verticegateway

  sudo systemctl stop verticevnc

  sudo systemctl stop vertice

  sudo sv stop nginx

  sudo sv stop unicorn

~~~

#### CentOS 7.2 Version 1.5.2

At the start, install Ruby2.3 and Runit for VerticeNilavu.

##### Ruby2.3

~~~bash

$ wget https://github.com/feedforce/ruby-rpm/releases/download/2.3.1/ruby-2.3.1-1.el7.centos.x86_64.rpm

$ sudo yum install -y libyaml

$ sudo rpm -ivh ruby-2.3.1-1.el7.centos.x86_64.rpm

~~~
##### Runit

~~~bash

$ curl -s https://packagecloud.io/install/repositories/imeyer/runit/script.rpm.sh | sudo bash

$ sudo yum install -y runit-2.1.1-7.el7.centos.x86_64

~~~

#### MegamVertice Packages

~~~bash

  cat << EOT > /etc/yum.repos.d/vertice.repo
[vertice]
name=vertice
baseurl=https://get.megam.io/repo/1.5.2/centos/7.2/testing
enabled=1
gpgcheck=0
EOT

  sudo yum update

  sudo yum install verticenilavu verticegateway nsqd vertice verticevnc

~~~

Lets focus on Configure [Vertice](http://docs.megam.io/configuration/vertice/) Packages.

~~~

To start MegamVertice

~~~bash

  sudo systemctl start nsqd

  sudo systemctl start nsqadmin

  sudo systemctl start nsqlookupd

  sudo systemctl start verticegateway

  sudo systemctl start verticevnc

  sudo systemctl start vertice

  runsvdir /var/service &

  sudo sv start nginx

  sudo sv start unicorn

~~~

To stop MegamVertice

~~~bash

  sudo systemctl stop nsqd

  sudo systemctl stop nsqadmin

  sudo systemctl stop nsqlookupd

  sudo systemctl stop verticegateway

  sudo systemctl stop verticevnc

  sudo systemctl stop vertice

  sudo sv stop nginx

  sudo sv stop unicorn

~~~

### Docker Images

Here you may be in a position to  use [Habitat - Docker images](https://github.com/megamsys/habitat_plans){: target="_blank"}. *Your choice is open to contribute habitat packages by intimating your interest to the [forum](https://forum.megam.io){: target="_blank"}.*
