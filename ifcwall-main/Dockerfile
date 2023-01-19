FROM ubuntu

# Install base utilities
RUN apt-get update && \
    apt-get install -y build-essential  && \
    apt-get install -y wget && \
    apt-get install ffmpeg libsm6 libxext6  -y && \
    # apt-get install libgl1 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install miniconda
ENV CONDA_DIR /opt/conda
RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh && \
     /bin/bash ~/miniconda.sh -b -p /opt/conda

# Put conda in path so we can use conda activate
ENV PATH=$CONDA_DIR/bin:$PATH
RUN echo "source activate base" > ~/.bashrc
ENV PATH /opt/conda/envs/base/bin:$PATH
COPY cloud.las .
COPY final1.py .
COPY lines.dxf .
COPY ref.xml .

RUN conda update -n base -c defaults conda \
    && conda install -c conda-forge --yes laspy \
    && conda install -c conda-forge --yes numpy \
    && conda install -c conda-forge --yes ezdxf \
    # && conda install -c conda-forge --yes open3d 
    && conda install pip \
    && conda install -c anaconda --yes scipy \
    && python -m pip install open3d

# RUN python -m pip install open3d 


ENTRYPOINT ["python", "final1.py"]