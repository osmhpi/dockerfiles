FROM debian:10 AS build

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
	apt-get install -y --no-install-recommends \
	cmake \
	g++ \
	git \
	ca-certificates\
	libfox-1.6-dev \
	libgdal-dev \
	libgl2ps-dev swig \
	libproj-dev \
	libxerces-c-dev \
	python3-setuptools \
	python3-dev \
	&& \
	apt-get autoremove -y && \
	apt-get clean -y && \
	rm -rf /var/lib/apt/lists/*

ENV DEBIAN_FRONTEND=false

ARG SUMO_TAG=1.4.0
ENV SUMO_HOME=/opt/sumo
WORKDIR $SUMO_HOME
RUN git clone --recursive -b "v$(echo $SUMO_TAG | sed 's/\./_/g')" --depth 1 https://github.com/eclipse/sumo . && \
	mkdir build/cmake-build && \
	cd build/cmake-build && \
	cmake ../.. && \
	make -j $(nproc) && \
	make DESTDIR=/build install

################################################################################

FROM debian:10

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
	apt-get install -y --no-install-recommends \
	ca-certificates \
	libfox-1.6 \
	libgdal20 \
	libgl2ps1.4 \
	libproj13 \
	libxerces-c3.2 \
	&& \
	apt-get autoremove -y && \
	apt-get clean -y && \
	rm -rf /var/lib/apt/lists/*

ENV DEBIAN_FRONTEND=false

COPY --from=build /build /
