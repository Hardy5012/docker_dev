# Docker 开发环境 #

  系统环境使用centos7. 各镜像的依赖关系，由下到上：
  
  + centos_gcc
  + centos_cmake
  + centos_git
  + centos_clang
  
## centos_gcc ##

  基础镜像为centos:7.5.1804, gcc版本为 8.1.0. 镜像大小508M
  
## centos_cmake ##
 
   cmake版本为3.12.0. 镜像大小 568M

## centos_git ##

  git版本为2.9.5. 镜像大小 773M
  
## centos_clang ##

  llvm 版本为6.0.1, 镜像大小 1.14G. 目前没有包含libc++.只编译了动态库.若想要静态库，可改为：
  
  > cmake -DCMAKE_INSTALL_PREFIX=/usr           \
      -DLLVM_ENABLE_FFI=ON                  \
      -DCMAKE_BUILD_TYPE=Release            \
      -DLLVM_BUILD_LLVM_DYLIB=ON            \
      -DLLVM_LINK_LLVM_DYLIB=ON             \
      -DLLVM_TARGETS_TO_BUILD="host;AMDGPU" \
      -Wno-dev ..                           \
