FROM centos:7.5.1804

ENV GCC_VERSION 8.1.0
ENV GMP_VERSION 6.1.2
ENV MPFR_VERSION 3.1.5
ENV MPC_VERSION 1.0.3

RUN yum -y update; yum clean all
RUN yum install -y make libmpc-devel mpfr-devel gmp-devel gcc gcc-c++ m4 bzip2; yum clean all 

RUN curl -fSL "https://ftp.gnu.org/gnu/gnu-keyring.gpg" -o /etc/gnu-keyring.gpg \
  && gpg -q --import /etc/gnu-keyring.gpg

RUN mkdir -p /usr/src/gmp \
  && curl -fSL "https://ftp.gnu.org/gnu/gmp/gmp-$GMP_VERSION.tar.xz" -o gmp.tar.xz \
  && curl -fSL "https://ftp.gnu.org/gnu/gmp/gmp-$GMP_VERSION.tar.xz.sig" -o gmp.tar.xz.sig \
  && gpg --batch --verify gmp.tar.xz.sig gmp.tar.xz \
  && tar xf gmp.tar.xz -C /usr/src/gmp --strip-components=1 \
  && rm -f gmp.tar.xz* \
  && cd /usr/src/gmp \
  && ./configure && make -j $(nproc) && make check && make install-strip \
  && cd .. && rm -rf gmp


RUN mkdir -p /usr/src/mpfr \
  && curl -fSL "https://ftp.gnu.org/gnu/mpfr/mpfr-$MPFR_VERSION.tar.xz" -o mpfr.tar.xz \
  && curl -fSL "https://ftp.gnu.org/gnu/mpfr/mpfr-$MPFR_VERSION.tar.xz.sig" -o mpfr.tar.xz.sig \
  && gpg --batch --verify mpfr.tar.xz.sig mpfr.tar.xz \
  && tar xf mpfr.tar.xz -C /usr/src/mpfr --strip-components=1 \
  && rm -f mpfr.tar.xz* \
  && cd /usr/src/mpfr \
  && ./configure && make -j $(nproc) && make check && make install-strip \
  && cd .. && rm -rf mpfr


RUN mkdir -p /usr/src/mpc \
  && curl -fSL "https://ftp.gnu.org/gnu/mpc/mpc-$MPC_VERSION.tar.gz" -o mpc.tar.xz \
  && curl -fSL "https://ftp.gnu.org/gnu/mpc/mpc-$MPC_VERSION.tar.gz.sig" -o mpc.tar.xz.sig \
  && gpg --batch --verify mpc.tar.xz.sig mpc.tar.xz \
  && tar xf mpc.tar.xz -C /usr/src/mpc --strip-components=1 \
  && rm -f mpc.tar.xz* \
  && cd /usr/src/mpc \
  && ./configure && make -j $(nproc) && make check && make install-strip  \
  && cd .. && rm -rf mpc


RUN mkdir -p /usr/src/gcc \
  && curl -fSL "http://ftpmirror.gnu.org/gcc/gcc-$GCC_VERSION/gcc-$GCC_VERSION.tar.xz" -o gcc.tar.xz \
  && curl -fSL "http://ftpmirror.gnu.org/gcc/gcc-$GCC_VERSION/gcc-$GCC_VERSION.tar.xz.sig" -o gcc.tar.xz.sig \
  && gpg --batch --verify gcc.tar.xz.sig gcc.tar.xz \
  && tar --xz -xvf gcc.tar.xz -C /usr/src/gcc --strip-components=1 \
  && rm -f gcc.tar.xz*\
  && cd /usr/src/gcc \
  && ./configure --disable-bootstrap --disable-multilib -enable-languages=c,c++ --prefix=/usr \
  && make -j $(nproc) \
  && make install-strip \
  && cd .. && rm -rf gcc


RUN echo "/usr/local/lib64" >> /etc/ld.so.conf.d/lib64.conf \
  && ldconfig -v