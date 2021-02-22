ARG NS3_PYTHON_VERSION=3.7
FROM python:${NS3_PYTHON_VERSION}-buster
ARG NS3_PYTHON_VERSION

RUN apt-get update && \
	DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
	libqt5printsupport5 \
	&& \
	apt-get autoremove -y && \
	apt-get clean -y && \
	rm -rf /var/lib/apt/lists/*

RUN python3 -c "from sys import version_info as v; pv = f'{v.major}.{v.minor}'; assert pv == '${NS3_PYTHON_VERSION}', f'Incompatible python version: {pv}'"

ARG NS3_VERSION=3.33
RUN pv="$(echo "${NS3_PYTHON_VERSION}" | tr -d '.')" && \
	pip3 install "https://github.com/osmhpi/python-wheels/releases/latest/download/ns-${NS3_VERSION}-cp${pv}-cp${pv}m-linux_x86_64.whl"

ENV PATH="${PATH}:/usr/local/lib/python${NS3_PYTHON_VERSION}/site-packages/ns/_/bin"
ENV PYTHONPATH="${PYTHONPATH}:/usr/local/lib/python${NS3_PYTHON_VERSION}/site-packages"
