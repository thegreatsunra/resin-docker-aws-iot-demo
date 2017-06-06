## resin-docker-aws-iot-demo

> AWS IoT messaging from a [resin.io][resin-link] Docker container

## Getting started

### Prerequisites

1) Install [node](https://nodejs.org/en/)
2) Install [git](https://git-scm.com/downloads)

## Set up AWS IoT

1) Sign up for AWS
2) Go to the AWS IoT home screen
3) Go to your Registry of Things
4) Create a new Thing
5) Name your Thing

### Create an AWD IoT "Thing" certificate

1) Choose "Security" from the menu
2) Click "Create Certificate"
3) Download "A certificate for this thing"
4) Download "A public key"
5) Download "A private key"
6) Download "A root CA for AWS IoT from Symantec"
7) Click the "Activate" button
8) Click "Done"

### Associate certificates with your project

1) Clone this repo
```bash
git clone https://github.com/thegreatsunra/docker-aws-iot-demo.git
cd resin-docker-aws-iot-demo
```

2) Move all the files you downloaded (the certificate, public key, private key, and root CA) from AWS IoT into the `certs/` folder of this project, and rename the files to `certificate.pem.crt`, `public.pem.key`, `private.pem.key`, and `root-CA.crt`

3) Open `.gitignore` in the root of this project and comment out the following lines to add your certs to your repo (this is terrible security but yolo)

```bash
# comment out these lines to add your certs and keys to your repo for resin.io:
*.crt
*.pem
*.key
```

4) Open `package.json` and find the `start` script (should be around line 30)

5) Update the value for `--host-name` to your "custom endpoint" on AWS IoT. You can find this value by clicking the "Settings" menu option on your AWS IoT home screen. It should look something like `xxxxxxxxxxxxxx.iot.xx-xxxx-x.amazonaws.com`

6) Commit your changes (again, we're committing your certs and keys to your repo, which is terrible security)

```bash 
git add -A
git commit -m 'Adding certs and keys to repo for resin.io because yolo'
```

### Set up resin.io and push your project to get it on a device

1) [Sign up for a resin.io account][signup-page]

2) Create an app on resin.io. Look at their [Getting Started tutorial][gettingStarted-link] for help

3) Set up a device (e.g. a Raspberry Pi 3) on resin.io

4) Add your resin.io application's remote repository to your project repo

```bash
# run this command from your resin-docker-aws-iot-demo folder
git remote add resin username@git.resin.io:username/myapp.git
```

5) Push your changes to the newly added remote to kick off a build:

```bash
git push resin master
```

It will take a few minutes for the code to push, build, deploy to your device, and for your device to start your app

## Confirm messages are streaming to AWS IoT

1) With your app running on your device, go to your AWS IoT home screen and click the "Test" menu option
2) Under "Subscribe to a topic" enter `awsIotDemo` as your "Subscription topic"
3) Click "Subscribe to topic"
4) Click the "awsIotDemo" menu item that appears beneath "Subscribe to a topic" in the left menu
5) You should see messages streaming in!

## License

The MIT License (MIT)

Copyright (c) 2017 Dane Petersen

[resin-link]:https://resin.io/
[signup-page]:https://dashboard.resin.io/signup
[gettingStarted-link]:http://docs.resin.io/#/pages/installing/gettingStarted.md
