# Cloudify PoC blueprints for OCCI and Puppet

[![Build Status](https://travis-ci.org/vholer/cloudify-occi-puppet-example.svg?branch=master)](https://travis-ci.org/vholer/cloudify-occi-puppet-example)

This is an example of two nodes deployment of Apache and PostgreSQL
started via FedCloud OCCI. Service deployment is managed by custom
Puppet interface which supports r10k (Puppetfile), Hiera bindings
and access to Cloudify context (ctx). Tested on CentOS 7.x.

## Standalone Cloudify

#### Setup OCCI CLI

```bash
yum install -y ruby-devel openssl-devel gcc gcc-c++ ruby rubygems
gem install occi-cli
```

#### Setup cloudify

```bash
make bootstrap
```

#### Run deployment

First get valid X.509 VOMS certificate into `/tmp/x509up_u1000` and
have `m4` installed.

```bash
source ~/cfy/bin/activate
make cfy-deploy
```

If succeeded, see deployed Apache endpoint URL. E.g.:

```bash
cfy local outputs
{
  "endpoint": {
    "url": "http://147.228.242.209"
  }
}
```

and open provided URL in your browser to see working
connection between webserver and database.

#### Destroy deployment

```bash
make cfy-undeploy
```

## Cloudify Manager

Blueprint is ready for Cloudify Manager.
