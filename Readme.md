# coderunner

http://coderunner.io

[JSbin](http://jsbin.com) for server-side languages. Run server-side code quickly and securely in the browser. Automatic dependency installation. Live code execution. Transparent revisioning. Powered by [docker](https://www.docker.com/).

![coderunner](https://i.cloudup.com/gCqIeOJSJY.png)

## Demo

![coderunner](https://i.cloudup.com/MBOXrwMRNl.gif)

## Design Goals

#### ⎈ Secure

Coderunner is designed to be secure. No user script should be able to jump outside its personal sandbox or modify any other script. All scripts run inside an isolated linux container and each package installer runs in a separate, shared linux container.

#### ✈ Fast

Coderunner is designed to provide immediate feedback. Most script runners use VMs to run server-side code securely. VMs are slow and CPU-intensive. Linux containers are fast and light-weight, offering the same kind of security that a VM provides.

#### ❁ Flexible

Many server-side script runners remove features of the language in order to keep the system secure. This makes the language much less powerful. With Coderunner, you have full access to everything the language provides.

#### ☯ Multilingual

Coderunner is designed to support many languages. Currently, Node.js is the only supported language, but it should be trivial to add additional scripting languages like Python, Ruby, PHP, etc.

#### ❖ Extendable

One of the upcoming goals of coderunner is to be more extendable by separating the API from the frontend. This will allow coderunner to support a variety of services.

## Development

### Local without docker (easy, insecure)

1. Install coderunner locally

    `git clone https://github.com/matthewmueller/coderunner`

2. Change directory into `coderunner`

    `cd ~/coderunner`

3. Install node modules & [components](https://github.com/visionmedia/component):

    `make install`

6. Start the server

    `node index.js --no-docker`

### VM with docker (more steps, secure)

In order to develop docker locally, you'll need to install VirtualBox, Vagrant and Git.

1. Install virtualbox from https://www.virtualbox.org/ (or use your package manager)
2. Install vagrant from https://www.vagrantup.com/ (or use your package manager)
3. Install git if you had not installed it before, check if it is installed by running git in a terminal window
4. Install coderunner locally:

    `git clone https://github.com/matthewmueller/coderunner`

5. Change directory to coderunner

    `cd coderunner`

6. Run vagrant from coderunner directory

    `vagrant up`

  Vagrant will download and install an ubuntu virtual machine containing:

  - ubuntu 12.04
  - docker
  - git
  - npm
  - node.js
  - coderunner

7. SSH into VM

    `vagrant ssh`

8. Change directory into `coderunner`

    `cd ~/coderunner`

9. Install node modules & [components](http://github.com/visionmedia/component):

    `make install`

10. Build all the docker images

    `make images`

11. Start the node-installer (using [mongroup](https://github.com/tj/node-mongroup))

    `mongroup start node-installer`

12. Start node server (use `node-dev index.js` if you want to autorestart on save)

    `node index.js`

13. Go to [http://localhost:8080](http://localhost:8080)

## Run code from your project


To add coderunner to your project, you can add the following icon pointing to your script:

    [![coderunner](https://i.cloudup.com/m1TVtFGGyk.png)](http://coderunner.io/:id/:revision)

Yielding:

[![coderunner](https://i.cloudup.com/m1TVtFGGyk.png)](http://coderunner.io/sw2s3ov6/2)

## Adding other languages

Coderunner makes it easy to add new languages. You will need to create two docker images, one for running and one for installing. The install container needs to be a web server that shares the installations volume (in node, `node_modules`) with all the runner container instances.

Take a look at [images/](https://github.com/MatthewMueller/coderunner/tree/master/images) for an example of how to add another language.

## TODO

This code is still in it's infancy. There's lots to do. Here's a few things I'd like to add:

#### Docker

- Better resource limiting in docker (memory, storage, & network)
- Better docker signal support (hopefully coming in docker 0.7, see [here](https://blog.docker.com/2013/08/websockets-dockerfile-upgrade-better-registry-support-expert-mode-and-more/).)
- Ship coderunner inside docker container ([docker inside docker](https://github.com/jpetazzo/dind/))

#### Features

- Easier language interface
- More languages
- User support with script history
- Multiple files
- Environment variables for easier sharing

## License

(The MIT License)

Copyright (c) 2013 Matt Mueller <mattmuelle@gmail.com>

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the 'Software'), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
