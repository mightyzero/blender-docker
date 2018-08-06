FROM ubuntu:18.04

# Blender's install_deps script requires sudo to function correctly
RUN apt-get update && apt-get install -y \
        ca-certificates \
        curl \
        sudo

ENV BLENDER_VER 2.79b

WORKDIR /blender-source

RUN curl --silent --output blender.tgz "http://download.blender.org/source/blender-${BLENDER_VER}.tar.gz"; \
    tar -C ./ -xzf blender.tgz; \
    rm blender.tgz;

WORKDIR ./blender-${BLENDER_VER}

RUN ./build_files/build_environment/install_deps.sh --with-all --skip-osl

WORKDIR ./build

RUN cmake ../
RUN make

ENV PATH /blender-source/blender-${BLENDER_VER}/build/bin:$PATH

CMD ["blender"]
