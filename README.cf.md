# Cloud Foundry Deployment

Install Cloud Foundry CLI: https://docs.developer.swisscom.com/cf-cli/install-go-cli.html


## Switch to project root and login to Cloud Foundry
```
$ cd my-project
$ cf login
```


## Create MongoDB instance
```
$ cf create-service mongodb small my-project-db
```

## Add Cloud Foundry application manifest
```
$ cat <<-EOD > manifest.yml
---
applications:
- name: my-project
  buildpack: https://github.com/cloudfoundry/buildpack-nodejs.git
  path: /tmp/build/bundle
  command: node main.js
  memory: 128MB
  host: my-project
  services:
  - my-project-db
  env:
    ROOT_URL: "http://my-project.scapp.io"
EOD 
```

## Add package.json to set node node version used in Cloud Foundry
```
$ cat <<-EOD > package.json.cf
{
  "engines": {
    "node": "4.8.2"
  }
}
EOD
```

## Add deploy script to packages.json
```
{
  "name": "my-project",
  "scripts": {
    "deploy": "rm -rf /tmp/build; meteor build /tmp/build --directory; chmod -R 777 /tmp/build; (cd /tmp/build/bundle/programs/server && npm install); cp package.json.cf /tmp/build/bundle/package.json; cp -av .profile.d /tmp/build/bundle/; cf push"
  },
}
```

## Set environment variables on instance startup
```
$ mkdir .profile.d
$ cat <<-EOD > .profile.d/init.sh
export MONGO_URL="`echo $VCAP_SERVICES | egrep -o 'mongodb:[^"]+' | head -1`"
EOD
```

## Run deploy script
```
$ npm run deploy
```
