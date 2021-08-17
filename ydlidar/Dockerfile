FROM ros:noetic-ros-core-focal

LABEL maintainer="Waipot Ngamsaad <waipotn@hotmail.com>"

SHELL ["/bin/bash", "-c"]

ENV DEBIAN_FRONTEND noninteractive

RUN  apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654

RUN sed -i -e 's/http:\/\/archive/mirror:\/\/mirrors/' -e 's/http:\/\/security/mirror:\/\/mirrors/' -e 's/\/ubuntu\//\/mirrors.txt/' /etc/apt/sources.list

RUN apt-get update && \
	apt-get upgrade -y && \
	apt-get install -y \ 
	build-essential \
    git 

RUN mkdir -p /ws/src && \
    cd /ws/src && \
	git clone https://github.com/YDLIDAR/ydlidar_ros.git && \
	cd /ws && \
	source /opt/ros/$ROS_DISTRO/setup.bash && \
	catkin_make install -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/opt/ros/$ROS_DISTRO -DCATKIN_ENABLE_TESTING=0 && \
	cd / && rm -rf /ws

RUN apt-get purge -y git && \
	apt-get autoremove -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

COPY ./start.launch /

CMD ["roslaunch", "--wait", "start.launch"]