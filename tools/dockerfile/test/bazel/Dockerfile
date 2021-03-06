# Copyright 2015 gRPC authors.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM gcr.io/oss-fuzz-base/base-builder

# -------------------------- WARNING --------------------------------------
# If you are making changes to this file, consider changing
# https://github.com/google/oss-fuzz/blob/master/projects/grpc/Dockerfile
# accordingly.
# -------------------------------------------------------------------------

# Install basic packages and Bazel dependencies.
RUN apt-get update && apt-get install -y software-properties-common python-software-properties
RUN add-apt-repository ppa:webupd8team/java
RUN apt-get update && apt-get -y install \
  autoconf \
  build-essential \
  curl \
  libtool \
  make \
  openjdk-8-jdk \
  vim

#====================
# Python dependencies

# Install dependencies

RUN apt-get update && apt-get install -y \
    python-all-dev \
    python3-all-dev \
    python-pip

# Install Python packages from PyPI
RUN pip install --upgrade pip==10.0.1
RUN pip install virtualenv
RUN pip install futures==2.2.0 enum34==1.0.4 protobuf==3.5.2.post1 six==1.10.0 twisted==17.5.0


#========================
# Bazel installation

# Must be in sync with tools/bazel
ENV BAZEL_VERSION 0.26.0

# The correct bazel version is already preinstalled, no need to use //tools/bazel wrapper.
ENV DISABLE_BAZEL_WRAPPER 1

RUN apt-get update && apt-get install -y wget && apt-get clean
RUN wget "https://github.com/bazelbuild/bazel/releases/download/$BAZEL_VERSION/bazel-$BAZEL_VERSION-installer-linux-x86_64.sh" && \
  bash ./bazel-$BAZEL_VERSION-installer-linux-x86_64.sh && \
  rm bazel-$BAZEL_VERSION-installer-linux-x86_64.sh


RUN mkdir -p /var/local/jenkins

# Define the default command.
CMD ["bash"]
