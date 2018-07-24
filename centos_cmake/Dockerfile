FROM  centos_gcc:v2

ENV CMAKE_VERSION 3.12
ENV CMAKE_SUB_VERSION 3.12.0

RUN mkdir -p /usr/src/cmake\
	&& curl -fSL "https://cmake.org/files/v$CMAKE_VERSION/cmake-$CMAKE_SUB_VERSION.tar.gz" -o cmake.tar.gz \
	&& tar -zxvf cmake.tar.gz -C /usr/src/cmake --strip-components=1 \
	&& rm -f cmake.tar.gz \
	&& cd /usr/src/cmake \
	&& ./bootstrap && make && make install \
	&& cd .. && rm -rf cmake
