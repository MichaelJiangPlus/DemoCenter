FROM ubuntu:16.04

RUN apt-get update && \
    apt-get install -y npm nodejs-legacy curl apt-transport-https git nano

RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg |  apt-key add -

RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" |  tee /etc/apt/sources.list.d/yarn.list

RUN apt-get update && \
    apt-get install -y yarn

RUN npm install -g n gitbook-cli

RUN n 8.11.1

# Configure environment
ENV CONDA_DIR /opt/conda
ENV PATH $CONDA_DIR/bin:$PATH
ENV SHELL /bin/bash
ENV NB_USER blackwalnut
ENV NB_UID 1000
ENV NB_PWD ZUCCli501
ENV HOME /home/$NB_USER

# Create jovyan user with UID=1000 and in the 'users' group
RUN useradd -m -s /bin/bash -N -u $NB_UID $NB_USER && \
    mkdir -p $CONDA_DIR && \
    chown $NB_USER $CONDA_DIR
    
RUN echo $NB_USER:$NB_PWD | chpasswd

RUN adduser $NB_USER sudo

RUN echo $NB_USER " ALL=(ALL:ALL) ALL" >> /etc/sudoers

RUN cat /etc/sudoers

RUN mkdir -p /home/blackwalnut/GitBook

RUN echo "cd /home/blackwalnut/GitBook \n gitbook serve" >> /home/blackwalnut/GitBook/start.sh

RUN chmod -R 777 /home/blackwalnut/GitBook/*

CMD ["sh", "/home/blackwalnut/GitBook/start.sh"]