# Project title

Short description of the project.

Config | Value
------------ | -------------
Exoscale Instance | my-project
URL | <http://my-project.ch>

## Technology

* [Meteor](https://www.meteor.com) is used as general application framework with MongoDB as database provider.
* [AngularJS](http://emberjs.com) because it supports fast prototyping with scaffolding and integrates nicely with meteor.
* [Materialize](http://materializecss.com) to stay sane while layouting and styling web applications as a developer.

## Prerequisites

You will need the following things properly installed on your computer.

* [Git](https://git-scm.com)
* [Node.js](https://nodejs.org) (with NPM)
* [Meteor >= 1.4](https://www.meteor.com)
* Meteor Up
  * `npm install -g mup`

## Installation

```sh
git clone git@github.com:[MY_PROJECT_REPO_URI]
cd my-project
meteor npm install
```

## Running / Development

`meteor`

* Visit your app at [http://localhost:3000](http://localhost:3000).

## Deploy to production

Deploy the meteor app

* `mup deploy`