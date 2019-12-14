FROM       ubuntu:18.04
MAINTAINER Jan Tulak "https://github.com/jtulak"

RUN apt-get update
RUN yes | unminimize

RUN apt-get install -y openssh-server mc tmux nmap rsync vim
RUN mkdir /var/run/sshd

RUN useradd -ms /bin/bash jtulak \
 && echo 'jtulak:jtulak' | chpasswd \
 && gpasswd -a jtulak sudo

RUN sed -ri 's/.*PasswordAuthentication\s+.*/PasswordAuthentication no/' /etc/ssh/sshd_config \
 && sed -ri 's/.*PermitRootLogin\s+.*/PermitRootLogin no/' /etc/ssh/sshd_config \
 && sed -ri 's/.*ChallengeResponseAuthentication\s+.*/ChallengeResponseAuthentication no/' /etc/ssh/sshd_config \
 && sed -ri 's/.*UsePAM\s+.*/UsePAM no/' /etc/ssh/sshd_config

RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# user directory will be mounted from the host
VOLUME ["/home/jtulak"]

EXPOSE 22

CMD    ["/usr/sbin/sshd", "-D", "-e"]
