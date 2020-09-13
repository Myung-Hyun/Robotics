#https://github.com/osrf/docker_images/blob/0b33e61b5bbed5b93b9fba2d5bae5db604ff9b58/ros/kinetic/ubuntu/xenial/ros-core/Dockerfile
#kinetic-ros-core, kinetic-ros-core-xenial


FROM ubuntu:xenial

#(RUN 명령은 환경을 구성하기 위해 패키지 등을 설치할 때 사용하는 명령이다. 우분투 위에 image layer를 만든다.)
# install packages
RUN apt-get update && apt-get install -q -y --no-install-recommends \
    dirmngr \
    gnupg2 \
    && rm -rf /var/lib/apt/lists/*

# setup keys
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654

# setup sources.list
RUN echo "deb http://packages.ros.org/ros/ubuntu xenial main" > /etc/apt/sources.list.d/ros1-latest.list

# setup environment(ENV: 초기 환경변수 설정)
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8
ENV ROS_DISTRO kinetic

# install ros packages
RUN apt-get update && apt-get install -y --no-install-recommends \
    ros-kinetic-ros-core=1.3.2-0* \
    && rm -rf /var/lib/apt/lists/*

# setup entrypoint (호스트OS의 파일 또는 디렉토리를 컨테이너 안의 경로로 복사, 즉 dockerfile build하는 위치에 ros_entrypoint.sh파일이 있어야 한다.)
COPY ./ros_entrypoint.sh /


# CMD와 ENTRYPOINT는 container 생성 후에, 실행하는 명령
# ENTRYPOINT 명령은 docker run으로 변경할 수 없고, CMD 명령은 변경할 수 있다. CMD 명령의 경우 default로 실행된다. 
ENTRYPOINT ["/ros_entrypoint.sh"]
CMD ["bash"]
