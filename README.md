# YouTransfer

[![GitHub version](https://badge.fury.io/gh/youtransfer%2Fyoutransfer.svg)](http://badge.fury.io/gh/youtransfer%2Fyoutransfer) [![npm version](https://badge.fury.io/js/youtransfer.svg)](http://badge.fury.io/js/youtransfer) [![Build Status](https://travis-ci.org/youtransfer/YouTransfer.svg?branch=master)](https://travis-ci.org/YouTransfer/YouTransfer) [![Maintainability](https://api.codeclimate.com/v1/badges/0af13d9a9eb8107a8417/maintainability)](https://codeclimate.com/github/YouTransfer/YouTransfer/maintainability) [![Test Coverage](https://api.codeclimate.com/v1/badges/0af13d9a9eb8107a8417/test_coverage)](https://codeclimate.com/github/YouTransfer/YouTransfer/test_coverage) [![Dependency Status](https://david-dm.org/youtransfer/youtransfer.svg)](https://david-dm.org/youtransfer/youtransfer) [![devDependency Status](https://david-dm.org/youtransfer/youtransfer/dev-status.svg)](https://david-dm.org/youtransfer/youtransfer#info=devDependencies) [![License](https://img.shields.io/github/license/youtransfer/youtransfer.svg)](http://www.apache.org/licenses/LICENSE-2.0) [![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/youtransfer/YouTransfer?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

YouTransfer is a simple but elegant self-hosted file transfer & sharing solution. It is an alternative to paid services like [Dropbox](http://dropbox.com) and [WeTransfer](http://wetransfer.com) by offering similar features but without limitations, price plans and a lengthy privacy policy. You remain in control of your files.

Created to be installed behind the firewall on private servers, YouTransfer aims to empower organisations and individuals that wish to combine easy-to-use file transfer tooling with security and control.

## Documentation

### Quick Start using Docker

If you wish to install YouTransfer in your own environment without any modifications, the [Docker image](http://hub.docker.com/r/remie/youtransfer/) is the most quick and easy approach. Simply [install docker](https://docs.docker.com/installation/) and run:

`docker pull remie/youtransfer:stable`

You can run the application with the following command:

````
docker run -d 
-v [path_to_upload_folder]:/opt/youtransfer/uploads 
-v [path_to_config_folder]:/opt/youtransfer/config 
-p 80:5000 remie/youtransfer:stable
````

### Using Docker container on Apache Webserver

If you deploy the environment to run on Apache Webserer, adequate settings are required. The following example reflect an Apache VirtualHost configuration with container running on the same host.

````
<VirtualHost>
<Proxy *>
    Order deny,allow
    Allow from localhost
</Proxy>
ProxyRequests Off
ProxyPreserveHost On
ProxyPass "/" "http://localhost:81" keepalive=On
ProxyPassReverse "/" "http://localhost:81"
RequestHeader set X-Forwarded-HTTPS "0"
</VirtualHost>
````

Note. For this, the container was started as follows (remember port 80 mostly already use by Apache, we take port 81):

````
docker pull remie/youtransfer:stable
docker run -d -v /opt/containerd/[upload_dir]:/opt/youtransfer/uploads -v /opt/containerd/[config_dir]:/opt/youtransfer/config -p 81:5000 remie/youtransfer:stable
````

You can now connect to YouTransfer by browsing to http://[docker_host_ip:port]/  
For more information on Docker deployment, please read the [Docker installation instructions](https://github.com/youtransfer/YouTransfer/wiki/docker).

### Additional documentation

You can find additional documentation (incl. installation and usage instructions) on the [GitHub Wiki](https://github.com/youtransfer/YouTransfer/wiki)
