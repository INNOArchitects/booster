# BoostCamp Starter Project

A starting point for BoostCamp prototypes.

> This is only tested with Linux.

## Table of Contents

* [Getting started guide for Meteor](#getting-started-with-meteor)
* [exoscale setup & deployment guide](#exoscale-deployment)
* [README template](#readme-template) to have consistent, minimal documentation for BoostCamp prototypes

## Prerequisites

* [GitHub Account](https://github.com/) to host the prototype code within the [INNOArchitects Organization](https://github.com/INNOArchitects)
* [exoscale Account](https://www.exoscale.ch/) to host the prototype

## Getting started with Meteor

### Prerequisites Meteor

* Meteor >= 1.4
  * <https://www.meteor.com/>
* Meteor Up
  * `npm install -g mup`

### Getting started

```bash
# Create the meteor app
meteor create my-project
cd my-project

# Install NPM dependencies
meteor npm install

# Run the app
meteor
```

## exoscale deployment

We use the [exoscale cloud](https://www.exoscale.ch/) to host prototypes. A new server can be setup in just a few minutes including single-command deployment.

* Add your [ssh key](https://portal.exoscale.ch/compute/keypairs) to the INNOArchitects Organization
* Add a [new instance](https://portal.exoscale.ch/compute/instances) with the following parameters
  * Hostname: my-project
  * Zone: CH-DK-2
  * Template: Linux Ubuntu 14.04 LTS 64-bit
  * Instance Type: Tiny (or faster if you really need it)
  * Disk: 10 GB (or bigger if you really need it)
  * Keypair: your ssh key
  * Security groups: default (ping, ssh, http [in/out] enabled)
* Connect to the new server via ssh to check if it is up and running
  * `ssh root@X.X.X.X`
* Add Meteor Up to your local project

```bash
cd my-project
mup init
```

* Open the Meteor Up configuration file mup.js and update the configuration

### Example configuration

```javascript
module.exports = {
  servers: {
    one: {
      host: '185.19.29.65', // IP of your exoscale server
      username: 'root',
      pem: '~/.ssh/id_rsa' // Path to your keypair
    }
  },

  meteor: {
    name: 'my-project', // Your project name
    path: '.', // Path to the project (in this example the config file is in the same directory as the meteor app)
    servers: {
      one: {},
    },
    buildOptions: {
      serverOnly: true,
      debug: true
    },
    env: {
      ROOT_URL: 'http://185.19.29.65', // IP of your exoscale server
      MONGO_URL: 'mongodb://localhost/meteor',
    },

    dockerImage: 'abernix/meteord:base',
    deployCheckWaitTime: 60,
    enableUploadProgressBar: true
  },

  mongo: {
    oplog: true,
    port: 27017,
    version: '3.4.1',
    servers: {
      one: {},
    },
  },
};
```

* Now you are able the set up the remote exoscale server with only one command. This script will run for a few minutes - it's ok. After this your server is all setup and you are ready to deploy your app.
  * `mup setup`
* Deploy the meteor app
  * `mup deploy`

## README template

```markdown
# TBD1

## TBD1.1

# TBD2

## TBD 2.1
```