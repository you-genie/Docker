FROM yougenie/base:cu110-torch-ubuntu20-devel
RUN sudo apt update; sudo apt-get install -y gcc g++
SHELL ["conda", "run", "-n", "torch", "/bin/bash", "-c"]
RUN conda install -y jupyterlab; conda install -c conda-forge tensorboard
ENV PATH /usr/local/cuda/bin:/$PATH
ENV TORCH_CUDA_ARCH_LIST "7.0"
CMD ["bash"]

