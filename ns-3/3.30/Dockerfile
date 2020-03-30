FROM debian:10

ARG PYTHON_VERSION=3.7

RUN apt-get update && \
	DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
	libpython${PYTHON_VERSION} \
	libqt5printsupport5 \
	python3-pip \
	&& \
	apt-get autoremove -y && \
	apt-get clean -y && \
	rm -rf /var/lib/apt/lists/*

RUN python3 -c "from sys import version_info as v; pv = f'{v.major}.{v.minor}'; assert pv == '${PYTHON_VERSION}', f'Incompatible python version: {pv}'"

ARG NS3_VERSION=3.30
RUN pip3 install https://github.com/osmhpi/python-wheels/releases/latest/download/ns-${NS3_VERSION}-py3-none-linux_x86_64.whl
