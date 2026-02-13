# How to test with ROS2

Docs: https://github.com/bondada-a/erobs/blob/humble-experimental/docs/Container_documentation.md


# Env vars

```bash
export ROS_DOMAIN_ID=0
```

# Docker setup

Start the server:
```bash
podman run --arch=amd64 -it --rm --network host --ipc=host --pid=host ghcr.io/bondada-a/beambot_img:latest bash
```

Inside the podman container:

```bash
source /root/ws/erobs/install/setup.bash && ros2 launch beambot beambot_bringup.launch.py use_fake_hardware:=true enable_vision:=false
```

Client side on the server image:
```bash
ros2 action send_goal /beambot_execution beambot_interfaces/action/MTCExecution "{full_json: '$(cat /root/ws/erobs/src/cms/tasks/beamtime/spincoat_to_hotplate.json)'}"
```

# Conda/pixi setup

```bash
pixi run ros2 topic list
pixi run ros2 node list
```

