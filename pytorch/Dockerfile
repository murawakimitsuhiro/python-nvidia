FROM nvidia/cuda:10.1-cudnn7-devel-ubuntu18.04

ARG PASSWORD

RUN apt-get update
RUN apt-get -y upgrade
RUN apt-get -y install vim
RUN apt-get -y install python3
RUN apt-get -y install python3-pip
RUN apt-get -y install libglib2.0-0 libsm6 libxrender1 libxext6

RUN apt-get -y install git openssh-server

RUN pip3 install torch torchvision
RUN pip3 install opencv-python

RUN ( echo "#!/bin/bash"; \
      echo ""; \
      echo "cp -R /tmp/.ssh /root/"; \
      echo "service ssh start"; \
      echo "tail -f /dev/null"; ) > /root/entrypoint.sh && \
    chmod +x /root/entrypoint.sh && \
    sed -i.bak 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    echo "PermitUserEnvironment yes" >> /etc/ssh/sshd_config && \
    ( echo ""; \
      echo "export PATH=/usr/local/nvidia/bin:/usr/local/cuda/bin:$PATH"; \
      echo "export LIBRARY_PATH=/usr/local/cuda/lib64/stubs:"; \
      echo "export LD_LIBRARY_PATH=/usr/local/nvidia/lib:/usr/local/nvidia/lib64"; \
    ) >> /root/.bashrc && \
    mkdir /root/.ssh && chmod 755 /root/.ssh && \
    ( echo "PATH=/usr/local/nvidia/bin:/usr/local/cuda/bin:$PATH"; \
      echo "LIBRARY_PATH=/usr/local/cuda/lib64/stubs:"; \
      echo "LD_LIBRARY_PATH=/usr/local/nvidia/lib:/usr/local/nvidia/lib64"; \
    ) >> /root/.ssh/environment

# ssh pass
RUN echo 'root:passwd' | chpasswd

CMD ["/root/entrypoint.sh"]

EXPOSE 22
