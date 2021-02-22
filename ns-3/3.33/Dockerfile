ARG PYTHON_VERSION=3.7
FROM python:${PYTHON_VERSION}-buster

RUN apt-get update && \
	DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
	libqt5printsupport5 \
	&& \
	apt-get autoremove -y && \
	apt-get clean -y && \
	rm -rf /var/lib/apt/lists/*

RUN python3 -c "from sys import version_info as v; pv = f'{v.major}.{v.minor}'; assert '${PYTHON_VERSION}'.startswith(pv), f'Incompatible python version: ${PYTHON_VERSION}'"

ARG NS3_VERSION=3.33
RUN pv="$(echo "${PYTHON_VERSION}" | sed -E 's/([0-9]+\.[0-9]+)\.[0-9]+/\1/g' | tr -d '.')" && \
	pip3 install "https://github.com/osmhpi/python-wheels/releases/latest/download/ns-${NS3_VERSION}-cp${pv}-cp${pv}m-linux_x86_64.whl"

ENV PATH="${PATH}:/usr/local/lib/python${PYTHON_VERSION}/dist-packages/ns/_/bin"
