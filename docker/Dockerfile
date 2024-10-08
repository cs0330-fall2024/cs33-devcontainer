FROM ubuntu:jammy

# set environment variables for tzdata
ARG TZ=America/New_York
ENV TZ=${TZ}

# include manual pages and documentation
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update &&\
  yes | unminimize

# install interactive programs (emacs, vim, nano, man, sudo, etc.)
RUN apt-get -y install\
 git\
 man\
 sudo\
 locales\
 clang-format\
 gdb\
 make\
 psmisc\
 nano\
 vim\
 dos2unix\
 valgrind\
 graphviz\
 gcc-multilib

# install dependencies for shell tests
RUN apt-get -y install\
 python3-pip\
 figlet\
 sysvbanner
RUN yes | pip install termcolor

# put reformat script in usr/bin
COPY .clang-format /usr/bin/.clang-format
COPY cs33_reformat /usr/bin/cs33_reformat
RUN chmod +rx /usr/bin/cs33_reformat

# set up default locale
RUN locale-gen en_US.UTF-8
ENV LANG=en_US.UTF-8

# remove unneeded .deb files
RUN rm -r /var/lib/apt/lists/*

# set up passwordless sudo for user cs33-user
RUN useradd -m -s /bin/bash cs33-user && \
  echo "cs33-user ALL=(ALL:ALL) NOPASSWD: ALL" > /etc/sudoers.d/cs33-init

# configure your environment
USER cs33-user
RUN rm -f ~/.bash_logout

WORKDIR /home/cs33-user
CMD ["/bin/bash", "-l"]
