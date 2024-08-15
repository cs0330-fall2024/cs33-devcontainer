FROM ubuntu:focal

# set environment variables for tzdata
ARG TZ=America/New_York
ENV TZ=${TZ}

# include manual pages and documentation
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update &&\
  yes | unminimize

# install GCC-related packages
RUN apt-get -y install\
 binutils-doc\
 gcc-doc\
 g++\
 g++-multilib\
 gdb\
 gdb-doc\
 glibc-doc\
 make\
 make-doc

# install clang-related packages
RUN apt-get -y install\
 clang\
 clang-10-doc\
 lldb\
 clang-format

# install interactive programs (emacs, vim, nano, man, sudo, etc.)
RUN apt-get -y install\
 git\
 git-doc\
 man\
 sudo

# set up libraries
RUN apt-get -y install\
 libreadline-dev\
 locales\
 libssl-dev

# install dependencies for shell tests
RUN apt -y install python3-pip
RUN yes | pip install termcolor

RUN apt -y install figlet\
  sysvbanner

# set up default locale
RUN locale-gen en_US.UTF-8
ENV LANG=en_US.UTF-8

# remove unneeded .deb files
RUN rm -r /var/lib/apt/lists/*

# set up passwordless sudo for user cs33-user
RUN useradd -m -s /bin/bash cs33-user && \
  echo "cs33-user ALL=(ALL:ALL) NOPASSWD: ALL" > /etc/sudoers.d/cs33-init

# create binary reporting version of dockerfile
RUN (echo '#\!/bin/sh'; echo 'echo 1') > /usr/bin/cs33-docker-version; chmod ugo+rx,u+w,go-w /usr/bin/cs33-docker-version

# configure your environment
USER cs33-user
RUN rm -f ~/.bash_logout

WORKDIR /home/cs33-user
CMD ["/bin/bash", "-l"]