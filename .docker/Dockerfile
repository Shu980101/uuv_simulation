# Use the official ROS1 Noetic base image
FROM osrf/ros:noetic-desktop-full

# Set environment variables
ENV DEBIAN_FRONTEND=noninteractive
ENV ROS_DISTRO=noetic
ENV CATKIN_WS=/root/catkin_ws

# Install dependencies
RUN apt-get update && apt-get install -y \
    python3-vcstool \
    python3-rosdep \
    git \
    ros-noetic-catkin \
    ros-noetic-catkin-tools \
    python3-catkin-tools \
    && rm -rf /var/lib/apt/lists/*

# Create and initialize the workspace
RUN mkdir -p $CATKIN_WS/src && \
    cd $CATKIN_WS/src && \
    git clone https://github.com/uuvsimulator/uuv_simulator.git && \
    cd $CATKIN_WS && \
    catkin init && \
    catkin build

# Source the workspace
RUN echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc && \
    echo "source $CATKIN_WS/devel/setup.bash" >> ~/.bashrc

# Set entrypoint
ENTRYPOINT ["/bin/bash"]

