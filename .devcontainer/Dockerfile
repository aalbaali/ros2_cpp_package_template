FROM althack/ros2:galactic-dev

ENV _colcon_cd_root=/workspace

ARG WORKSPACE

# Copy the list of packages into the container
COPY packages.txt /scripts/

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get -y update \
    # Install list of packages
    && xargs apt-get -y install --no-install-recommends < /scripts/packages.txt \
    && apt-get -y install software-properties-common \
    && add-apt-repository -y ppa:ubuntu-toolchain-r/test \
    && apt-get -y install --no-install-recommends g++-11 \
    && pip3 install --no-input gcovr \
    #
    # Clean up
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

ENV DEBIAN_FRONTEND=dialog

# Link the g++ binaries to g++-11 to make it the default compiler
# https://stackoverflow.com/questions/7832892/how-to-change-the-default-gcc-compiler-in-ubuntu
RUN update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-11 100
RUN update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-9 50
RUN update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-11 100
RUN update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 50
RUN update-alternatives --install /usr/bin/cpp cpp-bin /usr/bin/cpp-11 100
RUN update-alternatives --install /usr/bin/cpp cpp-bin /usr/bin/cpp-9 50
RUN update-alternatives --set g++ /usr/bin/g++-11
RUN update-alternatives --set gcc /usr/bin/gcc-11

# Set timezone
RUN ln -fs /usr/share/zoneinfo/Canada/Eastern /etc/localtime

CMD ["/bin/bash"]
