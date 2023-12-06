# mcsmanager-docker

Dockerfiles for [MCSManager](https://github.com/MCSManager/MCSManager)

## How To (Building docker image)
Making sure that you have installed docker.
1. Cloning that repository
2. Using command shell, redirecting to daemon or web folder
3. Running `docker build -t eterluu/mcsm-{daemon,web} .` (mcsm-{daemon,web} should be replaced by mcsm-daemon, mcsm-web or as you wanted)

## How to (Runnning docker image as a container)
Making sure that you have installed docker-compose and built the mcsm-web and mcsm-daemon images.
1. Using command shell, redirecting to daemon or web folder
2. Running `docker-compose up -d`