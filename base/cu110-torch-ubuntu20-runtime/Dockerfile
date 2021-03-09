# start from cuda110
FROM nvidia/cuda:11.0-runtime-ubuntu20.04
ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV PATH=/opt/conda/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# install packages
RUN apt-get update --fix-missing && yes | apt-get upgrade && apt-get -y install sudo wget curl bzip2 ca-certificates git vim && sudo apt-get clean

# Make SUDO MYUSER=genne (change the name)
ENV MYUSER genne
RUN adduser --disabled-password --gecos '' ${MYUSER} && adduser ${MYUSER} sudo && echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
USER ${MYUSER}
WORKDIR /home/${MYUSER}
RUN chmod a+rwx /home/${MYUSER}

# install Anaconda (change the anaconda version) change ANACONDA_PREFIX with archive/ if wants to install anaconda
ENV ANACONDA Miniconda3-latest-Linux-x86_64
ENV ANACONDA_PREFIX miniconda
RUN curl -O https://repo.anaconda.com/${ANACONDA_PREFIX}/${ANACONDA}.sh && bash ${ANACONDA}.sh -b && rm ${ANACONDA}.sh
ENV PATH /home/${MYUSER}/${ANACONDA_PREFIX}3/bin:$PATH
RUN conda update -n base -c defaults conda
RUN conda init
# RUN conda update anaconda && conda update --all

# install pytorch with conda. 
RUN conda create -n torch python=3.8 
SHELL ["conda", "run", "-n", "torch", "/bin/bash", "-c"]
RUN conda install pytorch torchvision cudatoolkit=11.0 -c pytorch

# some port options
EXPOSE 8888 6006
CMD ["bash"]
