# Introduction

A Web server is a program that uses HTTP (Hypertext Transfer Protocol) to serve the files that form Web pages to users, in response to their requests, which are forwarded by their computers' HTTP clients. Dedicated computers and appliances may be referred to as Web servers as well.

The process is an example of the client/server model. All computers that host Web sites must have Web server programs. Leading Web servers include Apache (the most widely-installed Web server), Microsoft's Internet Information Server (IIS) and nginx (pronounced engine X) from NGNIX. Other Web servers include Novell's NetWare server, Google Web Server (GWS) and IBM's family of Domino servers.

The primary function of a web server is to store, process and deliver web pages to clients. The communication between client and server takes place using the Hypertext Transfer Protocol (HTTP). Pages delivered are most frequently HTML documents, which may include images, style sheets and scripts in addition to text content.

A user agent, commonly a web browser or web crawler, initiates communication by making a request for a specific resource using HTTP and the server responds with the content of that resource or an error message if unable to do so. The resource is typically a real file on the server's secondary storage, but this is not necessarily the case and depends on how the web server is implemented.

While the primary function is to serve content, a full implementation of HTTP also includes ways of receiving content from clients. This feature is used for submitting web forms, including uploading of files.

Many generic web servers also support server-side scripting using Active Server Pages (ASP), PHP, or other scripting languages. This means that the behaviour of the web server can be scripted in separate files, while the actual server software remains unchanged. Usually, this function is used to generate HTML documents dynamically ("on-the-fly") as opposed to returning static documents. The former is primarily used for retrieving or modifying information from databases. The latter is typically much faster and more easily cached but cannot deliver dynamic content.

Web servers are not only used for serving the World Wide Web. They can also be found embedded in devices such as printers, routers, webcams and serving only a local network. The web server may then be used as a part of a system for monitoring or administering the device in question. This usually means that no additional software has to be installed on the client computer, since only a web browser is required (which now is included with most operating systems).

![Alt text](https://github.com/farashahamad/Apache-Web-Server/blob/master/Web%20Server.jpg?raw=true "Optional Title")

# Apache-Web-Server

Apache HTTP Server is free and open-source cross-platform web server software. Apache is developed and maintained by an open community of developers under the auspices of the Apache Software Foundation.

Apache HTTP Server is cross-platform, meaning that it is built for Unix-like systems (e.g., macOS, Linux and FreeBSD) as well as Windows.
Apache played a key role in the initial growth of the World Wide Web growing as the dominant HTTP server, and has remained most popular since April 1996. In 2009, it became the first web server software to serve more than 100 million websites.

As of July 2016, Apache remained the most widely used web server software, estimated to serve 46% of all active websites and 43% of the top million websites.

## Features
* Supports variety of features, many implemented as compiled modules which extend the core functionality.
* Server side programming language support – perl, python, Tcl, PHP.
* Authentication modules include mode_access, mod_auth, mod_digest, mod_gzip.
* SSL and TSL support (mod_ssl), proxy module (mod_proxy), URL rewriter (mod_rewrite), custom log file (mod_log_config), and filtering support (mod_include and mod_ext_filter)
* Compression method includes external extension module mod_gzip.
* ModSecurity is an open source intrusion detection and prevention engine for Web applications.
*Apache logs can be analyzed through web browser using free scripts such as AWStats/W3Perl or Visitors.
* Allows virtual hosting.
* Features configurable error messages, DBMS based authentication databases, and content negotiation.
* Supported by several GUIs.
* Supports password authentication and digital certificate authentication.
* Apache provides variety of multiprocessing modules (MPMs) which allows Apache to run in a process-based, hybrid (process and thread), or event-hybrid mode to better match the demands of each particular infrastructure.

## Important topics in Apache web server
### Installation
### Deployment
### Configuration
### Authentication
### Virtual Hosting
### Plug-in Configuration
### Logging
### Load balancer
### Error Codes
### Troubleshooting

## INSTALLATION
Apache httpd uses libtools and autoconf to create a build environment that looks like many other Open source projects.
#### Requirements
* APR and APR-Util
APR and APR-Util must be installed prior to building Apache httpd. Download latest versions of both unpack them into ./srclib/apr and ./srclib/apr-util and use ./configure - -with-included-apr option.

#### Perl-Compatible Regular Expressions Library (PCRE)
This library is required but no longer bundled with httpd. Download the source code, or install a Port or Package.

#### Disk Space
50 MB of temporary free disk space. After installation server occupies 10 MB of disk space.

#### ANSI-C Compiler and Build System
GNU C Compiler (GCC) from Free Software Foundation is recommended.

#### Accurate time keeping
ntpdate or xntpd programs are used which are based on NTP.

#### Perl 5 (Optional)
For some of the scripts like apxs or dbmmanage (which are written in Perl) the Perl 5 interpreter is required

#### Download
```
Lynx httpd:/httpd.apache.org/download.cgi
```
After downloading verify the version by testing the downloaded tarball against the PGP signature.

#### Extract
Uncompress and untar
```
gzip –d httpd-NN.tar.gz
tar xvf httpd-NN.tar
```
This will create a new directory under the current directory containing source code for distribution. Cd into the directory before proceeding with compiling the server.

#### Configuring Source Tree
Configuring the Apache source tree for the particular platform and personal requirement. This is done using the script configure included in the root directory of the distribution. To configure source tree using all the default options ./configure. To change the default options, configure accepts a variety of variables and command line options.
- - prefix – location where Apache is to be installed.
Also at this point, you can specify which features you want included in Apache by enabling or disabling modules. The modules are compiled as dynamic shared objects (DSO) which can be loaded or unloaded at runtime. Can also choose to compile modules statically by using the option - - enable-module=static
e.g. $ CC=”pgcc’ CFLAGS=”-O2” \
```
./configure - -prefix=/sw/pkg/apache 
- -enable-ldap=shared 
- -enable-lua=shared
```
#### Build
Build the various parts which form the Apache package by running $ make, this will require root privileges.

#### Customize
By editing configuration files under PREFIX/conf/.
```
$ vi PREFIX/conf/httpd.conf
```
#### Test
```
$ PREFIX/bin/apachectl –k start
```
You should be able to request your first document via the URL http://localhost/. The web page you see is located under the DocumentRoot which will usually be PREFIX/hdocs/.
```
$ PREFIX/bin/apachectl –k stop
```
#### Upgrading
The make install process will not overwrite any of the existing documents, log files, or configuration files. To upgrade across minor versions, start by finding the file config.nice in the build directory of the installed server or at the root of the source tree for your old install. This will contain the exact configure command line that you used to configure the source tree. Then to upgrade from one version to next, copy the config.nice file to the source tree of the new version, edit it to make the desired changes and then run.
```
$ ./config.nice
$ make
$ make install
$ PREFIX/bin/apachectl –k graceful –stop
$PREFIX/bin/apachectl –k start
```
Can pass additional arguments to config.nice, which will be appended to the original configure options.
```
$ ./config.nice - -prefix=/home/test/apache - -with-port=90
```

## CONFIGURATION

Root of Apache’s config directory at /etc/httpd/ with inside conf, conf.d, logs modules, run.

Conf directory holds the main apache configuration. Inside it’ll contain httpd.conf, magic and custom.

### httpd.conf
```
/etc/httpd/conf/httpd.conf 
```
This is the first configuration file apache will read, and it contains most of the settings for apache by default.

### magic 
```
/etc/httpd/conf/magic
```
Magic stores all information about MIME types (Multi-purpose Internet Mail Extensions). MIME types are essentially identifiers a web server and web client will use to indicate that a file is of a particular type.

### custom
Add an include directive at the end of httpd.conf
```
Include /etc/httpd/conf/custom/*.conf
```
### conf.d
```
/etc/httpd/conf.d/
```
It holds the module config files. The httpd.conf file will have the include directive that reads the files in this directory into the configuration right after a bunch of LoadModule directives.

### Logs
```
/etc/httpd/logs/
```
Logs is a symlink to where apache stores it’s main configuration files, /var/log/httpd.

### Modules
‘Modules’ is a symlink to /usr/lib/httpd/modules. Those are the libraries that apache reads as modules to add features like server-side include and PHP support.

### Run
Symlink to /var/run/httpd. This directory holds only one file, and it should be running when apache running. That file “httpd.pid” stores the main process id for apache.

### /etc/sysconfig


## AUTHENTICATION
Apache authentication can be configured to require web site visitors to login with a user id and password. The login dialog box which requests the user id and password is provided by the web browser at the request of Apache. Apache allows the configuration to be entered in it’s configuration files (i.e. main configuration file /etc/httpd/conf/httpd.conf, supplementary configuration files /etc/httpd/conf.d/component.conf or in a file which resides with in the directory to be password protected.

### Apache password file authentication
Directory protection using .htaccess and .htpasswd
1.	Editing the server configuration file to enable/allow a directory structure on the server to be password protected. <Directory> access permission statement need modification.
2.	The creation and addition of two files specifying the actual logins and passwords (.htaccess and .htpasswd)
Apache authentication uses the modules mod_auth and mod_access.
```
/etc/httpd/conf/httpd.conf
```
Default configuration disables the processing of .htaccess files for the system.
```
<Directory>
AllowOverride None
</Directory>
```
For a specified directory
```
<Directory /home/domain/public_html>
Allowoverride None
</Directory>
```
Change to specify directory to protect
```
<Directory /home/domain/public_html/membersonly>
Allowoverride All
</Directory>
```
Or
```
<Directory /home/domain/public_html/membersonly>
Allowoverride AuthConfig
</Directory>
```
Allowoverride Parameters: AuthConfig FileInfo Indexes Limits Options
The name of the “distributed” and user controlled configuration file .htaccess is defined with the directive
```
AccessFileName .htaccess
```
### Password protection by single login

1. Create the directory you want to password protect.
2. Create file /home/domain/public_html/membersonly/.htaccess in that directory that looks something like:
```
AuthName “Add your Login message here”
AuthType Basic
AuthUserFile /home/domain/public_html/membersonly/.htpasswd
AuthGroupFile /dev/null
Require user name-of-user
```
3. Create the password file /home/domain/public_html/membersonly/.htpasswd
```
htpasswd –c .htpasswd name-of-user
```
Add a new user to the existing password file:
```
htpasswd .htpasswd name-of-user
```
Password file protection, ownership and SELinux attirbutes.
```
File privileges: chmod ug+rw .htpasswd
File Onwership: chown apache.apache .htpasswd
SELinux file attributes: chcon –R –h – u system_u –r object_r –t httpd_config_t .htpasswd
```
Flexible password protection by group access permissions
1. Create a file .htgroup in that directory which contains the groupname and list of users.
```
member-users: user1 user2 user3 … etc
```
Where member-user is the name of the group

2. Modify .htaccess in the membersonly directory 
```
AuthName “Add your Login message here”
AuthType Basic
AuthUserFile /home/domain/public_html/membersonly/.htpasswd
AuthGroupFile /home/domain/public_html/membersonly/.htgroup
require group member-users
```
3. Create password file .htpasswd for each user as above
```
htpasswd –c /home/domain/public_html/membersonly/.htpasswd user1
htpasswd /home/domain/public_html/membersonly/.htpasswd user2
```
### Restrict access based on domain or IP address
```
Order deny, allow
Deny from all
Allow from allowable-domain.com
Allow from xxx.xxx.xxx
Deny from evil-domain.com
```
### Placing Authentication directives in httpd.conf exclusively instead of using .htaccess
The purpose of using “distriuted configuration file” .htaccess is so that users may control authentication. It can also be set in httpd.conf instead of .htaccess
```
…
…
<Directory /home/domain/public_html/membersonly>
Allowoverride AuthConfig
AuthName “Add your login message here”
AuthType Basic
AuthUserFile /home/domain/public_html/membersonly/.htpasswd
AuthGroupFile /dev/null
require user name-of-user
</Directory>
```

### Using LDAP for Apache Authentication
This authenticates using Apache 2.0/2.2 and the LDAP authentication modules on Linux and an LDAP server.

#### Apache LDAP modules:
LDAP modules should be enabled
```
Apache 2.0: mod_ldap, mod_auth_ldap
Apache 2.2: mod_ldap, mod_authnz_ldap
```
/etc/httpd/conf/httpd.conf

Apache 2.0
```
LoadModule ldap_module modules/mod_ldap.so
LoadModule auth_ldap_module modules/mod_auth_ldap.so
```
Apache 2.2
```
LoadModule ldap_module modules/mod_ldap.so
LoadModule authnz_ldap_module modules/mod_authnz_ldap.so
```
Apache Authentication Configuration
Apache 2.0
Authenticate to an Open LDAP server
httpd.conf
```
…
…
<Directory /var/www/html>
AuthType Basic
AuthName “Stooges Web Site: Login with email”
AuthLDAPURL ldap://ldap.yolinux.com:389/o=stooges?mail
require valid-user
</Directiry>

Or create the file /var/www/html/.htaccess


AuthName “Stooges Web Site: Login with email”
AuthType Basic
AuthLDAPURL ldap://ldap.your-domain.com:389/o=stooges?mail
require valids-user
```
Bind with a bind DN: (Password protected LDAP repository)
httpd.conf
```
…
…
<Directory /var/www/html>
AuthType Basic
AuthName “Stooges Web Site: Login with email”
AuthLDAPEnabled on
AuthLDAPURL ldap://ldap.your-domain.com:389/o=stooges?mail
AuthLDAPBindDN “cn=StoogeAdmin, o=stooges”
AuthLDAPBindPassword Secret1
require valid-user
</Directory>
…
…
```
Examples:
Require valid-user: Allow all users if authentication is correct.
Require user greg phil bob: Allow only greg phil bob to login.
Require group accounting: Allow only users in group “accounting” to authenticate.

Apache 2.2
Authenticate using Apache httpd 2.2 AuthzLDAP:
User authentication:
File httpd.conf
```
...
…
<Directory /var/www/html>
	AuthType Basic
	AuthName “Stooges Web Site: Login with user id”
	AuthBasicProvider ldap
	AuthLDAPAuthoritative on
	AuthLDAPURL ldap://ldap.your-domain.com:389/o=stooges?uid?sub
	AuthLDAPBindDN “cn=StoogeAdmin,o=stooges”
	AuthLDAPBindPAssword secret1
	Require ldap-user lary curley moe joe bob mary
</Directory>
…
..
```

There are two configurations for the directive AuthzLDAPAuthoritative
AuthzLDAPAuthoritative on (default)
```
…
Require ldap-user lary curley moe joe bob mary
AuthzLDAPAuthoritative off
…
Require valid-user
```

Group Authentication:
LDAP LDIF file:
dn: cn=users,ou=group,o=stooges
cn: users
objectClass: top
objectClass: posixGroup
gidNumber: 100
memberUid: larry
memberUid: moe

Apache configuration:
```
…
<Directory /var/www/html>
	Order deny,allow
	Deny from All
	AuthType Basic
	AuthName “Stooges Web Site: Login with user id”
	AuthBasicProvider ldap
	AuthzLDAPAuthoritative on
	AuthLDAPURL ldap://ldap.your-domain.com:389/o=stooges?uid?su
	AuthLDAPBindDN “cn=StoogeAdmin,o=stooges”
	AuthLDAPBindPassword secret1
	AuthLDAPGroupAttribute memberUid
	AuthLDAPGroupAttributeIsDN off
	Require ldap-group cn=users,ou=group,o=stooges
	Require ldap-attribute gidNumber=100
	Satisfy any
</Directory>
…
```
## SSL CONFIGURATION
* SSL Process works as follows:
1. Client connects to web server and gives a list of available ciphers.
2. Server picks the strongest cipher that both it and the client support, and sends back a certificate with its name and public encryption key, signed by a trusted Certificate Authority.
3. The client checks the certificate with the CA.
4. The client sends back a random number encrypted with the servers’ public key. Only the client knows the number, and only the server can decrypt it (using its private key).
5. Server and client use this random number to generate key material for the rest of the transaction.

* Getting required software:
```
openSSL and mod_ssl
yum install mod_ssl openssl
```
* Generate a self-signed certificate

Using OpenSSL we will generate a self-signed certificate. For production server you may want a key from Trusted Certificate Authority.

* Generate private key
``` 
openssl genrsa –out ca.key 2048
```
* Generate CSR
```
openssl req –new –key ca.key –out ca.csr
```
* Generate Self Signed Key
```
openssl x509 –req –days 365 –in ca.csr –signkey ca.key –out ca.crt
```
* Copy the files to the correct locations
```
cp ca.crt /etc/pki/tls/certs
cp ca.key /etc/pki/tls/private/ca.key
cp ca.csr /etc/pki/tls/private/ca.csr
(restorecon –RvF /etc/pki)
```
* Update apache SSL configuration file
```
vi +/SSLCertificateFile /etc/httpd.conf/ssl.conf
```
* Change paths to match where the key file is stored.
```
SSLCertificateFile /etc/pki/tls/certs/ca.crt
```
* Then set the correct path for the Certificate Key File a few lines below.
```
SSLCertificateKeyFile /etc/pki/tls/private/ca.key
```
* Quit and save the file and then restart apache
```
/etc/init.d/httpd restart
```
### Setting up the virtual hosts
Just as you set VirtualHosts for http on port 80 you do for https on port 443.
```
<virtualHost *:80>
	<Directory /var/www/vhosts/yoursite.com.httpdocs>
	AllowOverride All
	</Directory>
	DocumentRoot /var/www/vhosts/yoursite.com/httpdocs
	ServerName yoursite.com
</VirtualHost>
```
To add a sister site on port 443
```
NameVirtualHost *:443
<VirtualHost *:443>
	SSLEngine on
	SSLCertificateFIle /etc/pki/tls/certs/ca.crt
	SSLCertificareKeyFile /etc/pki/tls/private/ca.key
	<Directory /var/www/vhosts/yoursite.com/httpsdocs>
	AllowOverride All
	DocumentRoot /var/www/vhosts/yoursite.com/httpsdocs
	ServerName yoursite.com
</VirtualHost>
```
* Restart Apache

* Configuring the firewall
```
iptables –A INPUT –p tcp - -dport 443 –j ACCEPT
/sbin/service iptables save
iptables –L –v
```
### Troubleshooting
* Check server is actually running 
```
ps -ef |grep apache
ps -ef |grep httpd
```
* Check permission on your key and certificate files are set correctly, as well as permissions on your test HTML file and its parent directory.
* Check the logs, main server logs and SSL logs. Change LogLevel value in config file to ‘debug’ and test again.
* If the problem is the SSL connection, a useful tool is s_client, which is a diagnostic tool for troubleshooting TLS/SSL connections.
```
/usr/bin/openssl s_client –connect http://443
```

## VIRTUAL HOSTING
Virtual host refers to practice of running more than one website on a single machine.
Two types, IP-based (different IP for every web site) and name-based (multiple names running on each IP address)

### Setup Name Based Virtual Host
Create directory where you want to keep all your website’s files, under /var/www/html/. /var/www/html will be the default Document Root in Apache virtual configuration.

```
mkdir /var/www/html/example1.com/, mkdir /var/www/html/example2.com/
```

To set up Name based virtual hosting you need to tell Apache which IP you will be using to receive Apache requests for all the websites or domain names. Using NameVirtualHost directive in main configuration file.

```
vi /etc/httpd/conf/httpd.conf
```
```
NameVirtualHost 192.168.0.100:80
```

Add VirtualHost directives
```
<VirtualHost 192.168.0.100:80>
	ServerAdmin webmaster@example1.com
	DocumentRoot /var/www/html/example1.com
	ServerName www.example1.com
	ServerAlias 
ErrorLog logs/www.example1.com-error_log
	CustomLog logs/www.example1.com-access_log common
</VirtualHost>

<VirtualHost *:80>
	ServerAdmin webmaster@example2.com
	DocumentRoot /var/www/html/example2.com
	ServerName www.example2.com
	ErrorLog logs/www.example2.com-error_log
	CustomLog logs/www.example2.com-access_log common
</VirtualHost>
```

Check the syntax
```
httpd –t
```

Create a test page called index.html and add some content to the file.
```
vi /var/www/html/example1.com/index.html
```
```
<html>
     <head>
	<title>
	  www.example1.com
	</title>
     </head>
     <body>
                  <h1> Hello, Welcome to www.example1.com. </h1>
      </body>
</hmtl>
```
Similarly for example2.com and test the setup by accessing both the domains in a browser.

http://www.example1.com
http://www.example2.com

### Setup IP based Virtual Hosting
Must have more than one IP address/Port assigned to the server. It can be on a single NIC card (eg, eth0:1, eth0:2…) Multiple NIC cards can also be attached.
* Create Multiple IP Addresses on a Single Network Interface.
Purpose of implementing IP based virtual Hosting is to assign IP for each domain and that particular IP will not be used by any other domain.
This kind of set up is required when a website is running with SSL certificate or on different ports and IPs. And you can also run multiple instances of Apache on a single machine.
```
ifconfig
eth0 192.168.0.100
eth0:1 192.168.0.101
```

To assign a specific IP/Port to receive http requests, change the Listen directive in httpd.conf file.
```
vi /etc/httpd/conf/httpd.conf
# Listen 80
Listen 192.168.0.100:80
```
Create virtual host sections for both the domains.
```
<VirtualHost 192.168.0.100:80>
	ServerAdmin webmaster@example1.com
	DocumentRoot /var/www/html/example1.com
	ServerName www.example1.com
	ErrorLog logs/www.example1.com-error_log
	CustomLog logs/www.example1.com-access_log common
</VirtualHost>

<VirtualHost 192.168.0.101:80>
	ServerAdmin webmaster@example2.com
	DocumentRoot /var/www/html/example2.com
	ServerName www.example2.com
	ErrorLog logs/www.example2.com-error_log
	CustomLog logs/www.example2.com-access_log common
</VirtualHost>
```

## PLUG-IN

The Apache HTTP Server Plug-In proxies requests from an Apache HTTP Server to a WebLogic Server cluster or instance. The plug-in enhances an Apache installation by enabling WebLogic Server to handle load-balancing or requests that require the dynamic functionality of WebLogic Server. You target a WebLogic Server instance using the WebLogicHost and WebLogicPort parameters in the plug-in configuration file. You target a WebLogic Server cluster or group of non-clustered servers using the WebLogicCluster parameter.

The plug-in is intended for use in an environment where an Apache Server serves static pages, and another part of the document tree (dynamic pages best generated by HTTP Servlets or JavaServer Pages) is delegated to WebLogic Server, which may be operating in a different process, possibly on a different host. To the end user—the browser—the HTTP requests delegated to WebLogic Server still appear to be coming from the same source.

HTTP-tunneling, a technique that gives HTTP requests and responses access through a company's firewall, can operate through the plug-in.
The Apache HTTP Server Plug-In operates as an Apache module within an Apache HTTP Server. An Apache module is loaded by Apache Server at startup, and then certain HTTP requests are delegated to it. Apache modules are similar to HTTP servlets, except that an Apache module is written in code native to the platform.

## LOGGING
### General Configuration
The following general default configuration directives are specified in absence of specific virtual host container configuration.

**Default Logging Configuration**
 
Log level directive: This specifies log message severity. Default is “warn.”

``` 
&ast&astLogLevel warn&ast&ast
```
Table of Level Severities

| Severity | Description | Example |
| -------- | ----------- | ------- |
|emergency | Emergencies — system is unusable |	“Child cannot open lock file. Exiting” |
|alert	   | Immediate action required	      | “getpwuid: couldn’t determine user name from uid”|
|crit	   | Critical conditions	      | “socket: Failed to get a socket, exiting child”|
|error	   | Error conditions	              | “Premature end of script headers”|
|warn	   | Warning conditions	              | “child process 1234 did not exit, sending another SIGHUP”|
|notice	   | Normal but significant condition |	“httpd: caught SIGBUS, attempting to dump core in …”|
|info	   | Informational	              | “Server seems busy…”|
|debug	   | Debug-level messages	      | “opening config file …”|
|trace1-8  | Trace messages	              | “proxy: FTP: … ”|
