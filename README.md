Continuous Integration with Jenkins on Amazon EC2
=================================================

## Initial Setup

### Fixing Locales in Ubuntu 13.04 on Amazon EC2

```bash
sudo apt-get install language-pack-en
```

### Installing Jenkins

```bash
wget -q -O - http://pkg.jenkins-ci.org/debian/jenkins-ci.org.key | sudo apt-key add -
echo "deb http://pkg.jenkins-ci.org/debian binary/" | sudo tee -a /etc/apt/sources.list.d/jenkins.list
sudo apt-get update
sudo apt-get install jenkins
```

## Installing and Configuring Apache

### Installing Apache

```bash
sudo apt-get install apache2
sudo a2enmod proxy
sudo a2enmod proxy_http
```

### `/etc/apache2/sites-available/jenkins.conf`

```bash
<VirtualHost *:80>
	ServerName HOSTNAME
	ProxyRequests Off
	<Proxy *>
		Order deny,allow
		Allow from all
	</Proxy>
	ProxyPreserveHost on
	ProxyPass / http://localhost:8080/
</VirtualHost>
```

### Enabling `jenkins.conf`

```bash
sudo a2ensite jenkins
sudo service apache2 reload
```

## Installing Java / Maven / Git

```bash
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java7-installer maven git-core
```