FROM  centos_git:2.9.5

ENV LLVM_VERSION 6.0.1
RUN yum -y update; yum clean all
RUN yum install -y libffi libffi-devel && yum clean all

RUN mkdir -p /usr/src/llvm/llvm && cd /usr/src/llvm\
&& curl -fSL "http://llvm.org/releases/$LLVM_VERSION/llvm-$LLVM_VERSION.src.tar.xz" -o llvm.tar.xz \
&& curl -fSL "http://llvm.org/releases/$LLVM_VERSION/cfe-$LLVM_VERSION.src.tar.xz" -o cfe.tar.xz \
&& curl -fSL "http://llvm.org/releases/$LLVM_VERSION/compiler-rt-$LLVM_VERSION.src.tar.xz" -o compiler.tar.xz \
&& tar --xz -xvf llvm.tar.xz \
&& cd llvm-$LLVM_VERSION.src \
&& tar -xf ../cfe.tar.xz -C tools && tar -xf ../compiler.tar.xz -C projects \
&& mv tools/cfe-$LLVM_VERSION.src tools/clang && mv projects/compiler-rt-$LLVM_VERSION.src projects/compiler-rt\
&& mkdir -v build && cd build \
&& CC=gcc CXX=g++                              \
cmake -DCMAKE_INSTALL_PREFIX=/usr           \
      -DLLVM_ENABLE_FFI=ON                  \
      -DCMAKE_BUILD_TYPE=Release            \
      -DBUILD_SHARED_LIBS=ON            \
      -DLLVM_TARGETS_TO_BUILD="host;AMDGPU" \
      -Wno-dev ..                           \
&& make install \
&& rm -rf /usr/src/llvm