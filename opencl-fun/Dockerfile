#
#  Copyright (C) 2016 Intel Corporation
#
#  This program is free software; you can redistribute it and/or
#  modify it under the terms of the GNU General Public License
#  as published by the Free Software Foundation; either version 2
#  of the License, or (at your option) any later version.
#
#  This program is distributed in the hope that it will be useful,
#  but WITHOUT ANY WARRANTY; without even the implied warranty of
#  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#  GNU General Public License for more details.
#
#  You should have received a copy of the GNU General Public License
#  along with this program; if not, write to the Free Software
#  Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA  02110-1301, USA.
#

FROM ubuntu:16.04

# Ensure packages are current, then install dependencies
RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y vim procps wget libmnl0


RUN apt-get update && apt-get install -y --no-install-recommends \
        ethtool \
 	ibutils \
	ibverbs-utils \ 
 	infiniband-diags \
        iproute2 \
        pciutils \
        libnl-route-3-200 \
        kmod \
	libmlx4-1 \
        libnuma1 \
        lsb-release \
        lsof \
        net-tools \
	open-iscsi \
	perftest \
        perl \
        python-libxml2 \
	rdmacm-utils \
	targetcli \
	tgt \
        wget && \
        rm -rf /var/lib/apt/lists/*

RUN apt-get update

RUN apt-get install -y autoconf dpatch debhelper tcl chrpath autotools-dev graphviz libgfortran3 automake flex pkg-config gfortran m4 swig tk bison libltdl-dev

RUN apt-get update && \
    apt-get install -y p7zip



ENV HASHCAT_VERSION        hashcat-3.6.0
ENV HASHCAT_UTILS_VERSION  1.8


RUN mkdir /hashcat
RUN cd /hashcat && \
    wget --no-check-certificate https://hashcat.net/files_legacy/${HASHCAT_VERSION}.7z && \
    7zr x ${HASHCAT_VERSION}.7z && \
    rm ${HASHCAT_VERSION}.7z

RUN cd /hashcat && \
    wget https://github.com/hashcat/hashcat-utils/releases/download/v${HASHCAT_UTILS_VERSION}/hashcat-utils-${HASHCAT_UTILS_VERSION}.7z && \
    7zr x hashcat-utils-${HASHCAT_UTILS_VERSION}.7z && \
    rm hashcat-utils-${HASHCAT_UTILS_VERSION}.7z

RUN ln -s /hashcat/${HASHCAT_VERSION}/hashcat64.bin /usr/bin/hashcat

RUN ln -s /hashcat/hashcat-utils-${HASHCAT_UTILS_VERSION}/bin/cap2hccapx.bin /usr/bin/cap2hccapx
ENV DEBIAN_FRONTEND="noninteractive"
RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections
RUN apt-get install -y nvidia-opencl-icd-384
