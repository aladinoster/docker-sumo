FROM continuumio/miniconda3

# Set the ENTRYPOINT to use bash
# (this is also where you’d set SHELL,
# if your version of docker supports this)
# ENTRYPOINT ["/bin/bash", "-c"]

# Open ports
EXPOSE 5000

# Libraries + Compiler
RUN apt-get update && apt-get install -y \
    wget bzip2 ca-certificates \
    xz-utils \
    build-essential \ 
    curl \   
    git \
    nano \
    libxerces-c-dev \
    libfox-1.6-dev \
    libxqilla-dev \
    libgdal-dev \
    libproj-dev \
    libgl2ps-dev \
    swig \
    aptitude \
    libpq-dev && \
    rm -rf /var/lib/apt/lists/* \
    && curl -SL http://releases.llvm.org/9.0.0/clang+llvm-9.0.0-x86_64-linux-gnu-ubuntu-18.04.tar.xz \
    | tar -xJC . && \
    mv clang+llvm-9.0.0-x86_64-linux-gnu-ubuntu-18.04 clang_9.0.0 && \
    echo 'export PATH=/clang_9.0.0/bin:$PATH' >> ~/.bashrc && \
    echo 'export LD_LIBRARY_PATH=/clang_9.0.0/lib:$LD_LIBRARY_PATH' >> ~/.bashrc

# Clone
RUN git clone --recursive https://github.com/eclipse/sumo

# Setting home directory
WORKDIR /sumo/

# Entry point
ENV TINI_VERSION v0.16.1
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini

ENTRYPOINT [ "/usr/bin/tini", "--" ]
CMD [ "/bin/bash" ]

# Conda install
RUN ["/bin/bash","-c","conda install -y -c conda-forge cmake"]

# Sumo configs 
RUN export SUMO_HOME="$PWD/sumo"

# Build sumo 
RUN mkdir -p /sumo/build/cmake-build && cd /sumo/build/cmake-build && \
    cmake ../.. && \ 
    make -j$(nproc)