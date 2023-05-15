# Installing ros through docker with GUI applications

Here are some commands to install ros that worked for me.

(I'm currently running ros on a laptop turning with Ubuntu 22.04)

## Docker installation

First of all, you'll need to get a proper Docker instance running on your computer.

Please follow the steps described here: https://docs.docker.com/engine/install/ubuntu/.

## Launching a ros container

These commands will create a docker container running the `osrf/ros:noetic-desktop-full` image.
You may find a more suitable image on https://registry.hub.docker.com/r/osrf/ros.

```bash
sudo docker run -it \
    --privileged \
    --name=ros_noetic \
    --user=$(id -u $USER):$(id -g $USER) \
    --env="DISPLAY" \
    --env="QT_X11_NO_MITSHM=1" \
    --env="LIBGL_ALWAYS_SOFTWARE=1" \
    --volume="/etc/group:/etc/group:ro" \
    --volume="/etc/passwd:/etc/passwd:ro" \
    --volume="/etc/shadow:/etc/shadow:ro" \
    --volume="/etc/sudoers.d:/etc/sudoers.d:ro" \
    --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" \
    -u root \
    osrf/ros:noetic-desktop-full \
    bash
```
## Running the container

```bash
sudo docker exec -it -u root <container-id-or-name> bash
```

You may want to add the `source /opt/ros/<your-ros-version>/setup.bash` command in `/root/.basrc` to enable the ros command by default on all your terminals.

Anyway, it's up to you.

Good luck :)
