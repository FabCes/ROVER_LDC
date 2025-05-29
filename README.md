#  Starting the Driver

To launch the necessary nodes to operate the rover, follow the steps below:

##  1. Pull Required Docker Images

If the drone's image has been reset, otherwise you can skip to step 3, download the necessary Docker images by running:

```bash
docker compose pull
```

##  2. Flash the Correct Firmware

Flash the correct firmware using the following command:

```bash
docker stop rosbot microros || true && docker run \
--rm -it --privileged \
husarion/rosbot:humble-0.6.1-20230712 \
flash-firmware.py /root/firmware.bin
```

##  3. Start the ROS Containers

Start the `rosbot` and `microros` containers in the background:

```bash
docker compose up -d rosbot microros
```

At this point, all required nodes should be running.

##  4. Set ROS Domain ID (if using rosbot container terminals)

If you're not using terminals from within the `rosbot` image, remember to set the correct `ROS_DOMAIN_ID`, since all nodes run with `ID=1`:

```bash
export ROS_DOMAIN_ID=1
```

##  5. Check Available Topics

You should now be able to list all active topics using:

```bash
ros2 topic list
```
