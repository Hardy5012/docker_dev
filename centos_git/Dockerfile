FROM  centos_cmake:3.12

ENV GIT_VERSION 2.9.5

RUN yum -y update; yum clean all
RUN yum install -y openssl-devel curl-devel  expat-devel gettext-devel zlib-devel perl-ExtUtils-MakeMaker ; yum clean all

RUN mkdir -p /usr/src/git \
	&& curl -fSL "https://www.kernel.org/pub/software/scm/git/git-$GIT_VERSION.tar.xz" -o git.tar.xz \
	&& tar --xz -xvf git.tar.xz -C /usr/src/git --strip-components=1 \
	&& rm -f git.tar.xz \
	&& cd /usr/src/git && make prefix=/usr/local/git  all && make prefix=/usr/local/git install \
	&& cd .. && rm -rf git \
	&& echo "export PATH=/usr/local/git/bin:$PATH" >>  ~/.bashrc