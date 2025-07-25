# micro-ROS + PlatformIO Development Container

## Overview

This repository provides a [VSCode devcontainer](https://code.visualstudio.com/docs/remote/containers) configuration to facilitate the development of [micro-ROS](https://micro.ros.org/) applications using [PlatformIO](https://platformio.org/). With this setup, you can work on micro-ROS projects without needing to install additional software directly on your host machine.

## Features

- **Preconfigured Development Environment**: The devcontainer is built upon the official micro-ROS rolling Docker image, with pre-installed extensions and dependencies for PlatformIO, along with USB passthrough support.
- **Project Mounting**: The `projects` folder is mounted within the container as the default PlatformIO project directory, allowing you to manage and develop your micro-ROS applications conveniently in this location.
- **Agent Communication Options**: This configuration includes a `docker-compose.yml` file to easily start the micro-ROS agent for device communication, available in two modes:
  - `serial-agent`: Enables serial communication with micro-ROS applications, defaulting to USB port `/dev/ttyUSB0`.
  - `udp-agent`: Allows network-based communication with micro-ROS applications via UDP, defaulting to port `9999`.

> [!NOTE]
> - The default `ROS_DOMAIN_ID` is set to `42`. You can adjust this value in both the `docker-compose.yml` and `devcontainer.json` files as needed.
> - By default, the internal user within the container is set to `vscode`. This can be modified if a different user setup is preferred.
> - To connect your development board, you may need to modify the port mounting configuration in `devcontainer.json`, which defaults to ttyUSB0.

## Usage

1. Clone this repository and open it in VSCode.
2. When prompted, reopen the repository in the container to initialize the devcontainer environment.
3. Develop your micro-ROS applications in the `projects` directory.
4. Use `docker-compose` to launch the desired micro-ROS agent as per your communication requirements.

Happy coding!
