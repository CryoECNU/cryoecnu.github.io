---
layout: post
title: 编译netcdf和mpich
date: 2021-10-09
categories: blog
description: 
tags: [Software, netcdf, mpich, compile]
header-img: img/top.png    #这篇文章标题背景图片
---

在MAC OS下面，不管是MACPORTS还是HOMEBREW安装的gcc、netcdf、mpich包，安装的时候都没问题，但是用来编译其他程序（比如编译VIC模型）的时候总报莫名其妙的错误。没办法，只好自己编译NETCDF和MPICH库了。

为了图个方便，使用NETCDF-4.1.3，因为再往后的版本就是C和FORTRAN版本分开了，麻烦些。

另外，经过各种尝试，gcc10以上的编译NETCDF4.1.3会报错。所以建议VIC都用GCC9 ～ GCC6版本。这里以homebrew安装的GCC9为例，写了一个bash脚本来简化安装。有时间再试试看windows下面如何编译VIC模型。


```console

export FC=gfortran-9
export F90=gfortran-9
export F77=gfortran-9
export CC=gcc-9
export CXX=g++-9

echo 'FC  = gfortran-9'
echo 'F90 = gfortran-9'
echo 'F77 = gfortran-9'
echo 'CC  = gcc-9'
echo 'CXX = g++-9'

export install_path=[/path/to/gcc_libs] # set to yours

echo "All libs will installed into ${install_path}"

export make_check=false #true or false

export compile_zlib=false
export compile_hdf5=false
export compile_netcdf4=false
export compile_mpich=true

export zlib_label=zlib-1.2.7
export hdf5_label=hdf5-1.8.19
export netcdf4_label=netcdf-4.1.3
export mpich_label=mpich-3.3

#====================MAY NOT BE CHANGED==============

#----------------------------------------------------

if [[ $compile_zlib = true ]]

then

echo 'Compile zlib ...'
 
if [[ ! -d ${zlib_label} ]]
then
    echo "${zlib_label} does not exist on your filesystem."
    tar -zxvf ${zlib_label}.tar.gz
    echo "unzip ${zlib_label}.tar.gz ..."
fi

cd ${zlib_label}

echo "enter zlib-1.2.7 ..."

./configure --prefix=${install_path}

make
test "$make_check" = true && make check
make install

echo 'zlib compiled  ...'

cd ..

fi

#----------------------------------------------------

if [[ $compile_hdf5 = true ]]

then

echo 'Compile hdf5 ...'

if [[ ! -d ${hdf5_label} ]]
then
    echo "${hdf5_label} does not exist on your filesystem."
    tar -zxvf ${hdf5_label}.tar.gz
    echo "unzip ${hdf5_label}.tar.gz ..."
fi

cd ${hdf5_label}

echo "enter ${hdf5_label} ..."

./configure --prefix=${install_path} --with-zlib=${install_path} --enable-hl

make
test "$make_check" = true && make check
make install

echo 'hdf5 compiled  ...'

cd ..

fi

#----------------------------------------------------

if [[ $compile_netcdf4 = true ]]

then

echo 'Compile netcdf4 ...'

if [[ ! -d ${netcdf4_label} ]]
then
    echo "${netcdf4_label} does not exist on your filesystem."
    tar -zxvf ${netcdf4_label}.tar.gz
    echo "unzip ${netcdf4_label}.tar.gz ..."
fi

cd ${netcdf4_label}

echo "enter ${netcdf4_label} ..."

./configure --prefix=${install_path} CPPFLAGS="-I${install_path}/include" LDFLAGS="-L${install_path}/lib" --enable-netcdf4 --enable-large-file-tests

make
test "$make_check" = true && make check
make install

echo 'netcdf4 compiled  ...'

cd ..

fi

#----------------------------------------------------

if [[ $compile_mpich = true ]]

then

echo 'Compile mpich ...'

if [[ ! -d ${mpich_label} ]]
then
    echo "${mpich_label} does not exist on your filesystem."
    tar -zxvf ${mpich_label}.tar.gz
    echo "unzip ${mpich_label}.tar.gz ..."
fi

cd ${mpich_label}

echo "enter ${mpich_label} ..."

unset F90
unset F90FLAGS

./configure --prefix=${install_path}

make
make install

cd ..

fi

```