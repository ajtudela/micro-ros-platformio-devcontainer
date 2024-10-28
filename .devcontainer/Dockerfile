FROM microros/base:humble
ARG USERNAME=USERNAME
ARG USER_UID=1000
ARG USER_GID=$USER_UID

LABEL maintainer="ajtudela@gmail.com"
LABEL version="1.0"
LABEL description="A container for developing micro-ROS + PlatformIO applications in a VSCode"
LABEL license="Apache-2.0"

# Delete user if it exists in container (e.g Ubuntu Noble: ubuntu)
RUN if id -u $USER_UID ; then userdel `id -un $USER_UID` ; fi

# Create the user
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# Install required packages
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get upgrade -y && apt-get -y install --no-install-recommends \
    ssh \
    udev \
    python3-pip \
    python3-venv

# Setup udev rules for PlatformIO
RUN curl -fsSL https://raw.githubusercontent.com/platformio/platformio-core/develop/platformio/assets/system/99-platformio-udev.rules | sudo tee /etc/udev/rules.d/99-platformio-udev.rules
RUN service udev restart
RUN usermod -a -G dialout $USERNAME
RUN usermod -a -G plugdev $USERNAME

# Source ROS environment automatically
RUN echo "source /opt/ros/$ROS_DISTRO/setup.bash" >> /home/$USERNAME/.bashrc

# Change to new user
ENV SHELL /bin/bash
USER $USERNAME
ENTRYPOINT ["/ros_entrypoint.sh"]
CMD ["/bin/bash"]