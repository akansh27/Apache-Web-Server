# Introduction

A Web server is a program that uses HTTP (Hypertext Transfer Protocol) to serve the files that form Web pages to users, in response to their requests, which are forwarded by their computers' HTTP clients. Dedicated computers and appliances may be referred to as Web servers as well.

The process is an example of the client/server model. All computers that host Web sites must have Web server programs. Leading Web servers include Apache (the most widely-installed Web server), Microsoft's Internet Information Server (IIS) and nginx (pronounced engine X) from NGNIX. Other Web servers include Novell's NetWare server, Google Web Server (GWS) and IBM's family of Domino servers.

The primary function of a web server is to store, process and deliver web pages to clients. The communication between client and server takes place using the Hypertext Transfer Protocol (HTTP). Pages delivered are most frequently HTML documents, which may include images, style sheets and scripts in addition to text content.

A user agent, commonly a web browser or web crawler, initiates communication by making a request for a specific resource using HTTP and the server responds with the content of that resource or an error message if unable to do so. The resource is typically a real file on the server's secondary storage, but this is not necessarily the case and depends on how the web server is implemented.

While the primary function is to serve content, a full implementation of HTTP also includes ways of receiving content from clients. This feature is used for submitting web forms, including uploading of files.

Many generic web servers also support server-side scripting using Active Server Pages (ASP), PHP, or other scripting languages. This means that the behaviour of the web server can be scripted in separate files, while the actual server software remains unchanged. Usually, this function is used to generate HTML documents dynamically ("on-the-fly") as opposed to returning static documents. The former is primarily used for retrieving or modifying information from databases. The latter is typically much faster and more easily cached but cannot deliver dynamic content.

Web servers are not only used for serving the World Wide Web. They can also be found embedded in devices such as printers, routers, webcams and serving only a local network. The web server may then be used as a part of a system for monitoring or administering the device in question. This usually means that no additional software has to be installed on the client computer, since only a web browser is required (which now is included with most operating systems).

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
