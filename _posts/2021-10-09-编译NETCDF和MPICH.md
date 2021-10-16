---
layout: post
title: 编译netcdf、mpich和Jasper库
date: 2021-10-09
categories: blog
description: 
tags: [Software, netcdf, mpich, jasper, compile]
header-img: img/top.png    #这篇文章标题背景图片
---

在MAC OS下面，不管是MACPORTS还是HOMEBREW安装的gcc、netcdf、mpich包，安装的时候都没问题，但是用来编译其他程序（比如编译VIC模型）的时候总报莫名其妙的错误。没办法，只好自己编译NETCDF、MPICH等库。优点是可以确保编译所有库都用的相同编译器，缺点是麻烦且又些耗时间。需要注意的是NETCDF库，要是图方便其实也可以使用NETCDF-4.1.3，因为再往后的版本就是C和FORTRAN版本分开了，要编译两个，会麻烦些。另外，要注意，gcc新版本编译NETCDF4.1.3会报错。所以建议都用<span style="color:red">**GCC7**</span>。

这里以homebrew安装的GCC7为例，写了一个bash脚本来简化安装一些常用的库：NETCDF、MPICH等。为了让NETCDF支持NC4，还需要先编译zlib、szip和hdf5。

NETCDF的编译顺序：

* szip or zlib
* zlib or szip
* hdf5
* netcdf-c
* netcdf-fortran

MPICH可以在NETCDF之前编译，也可以之后编译。两者是独立的。


```

#----------------------------------------------------
#------------- A script to compile libs -------------
#-------------    by Kang Wang, ECNU    -------------
#-------------      Oct, 2021           -------------
#----------------------------------------------------

export FC=gfortran-7
export F90=gfortran-7
export F77=gfortran-7
export CC=gcc-7
export CXX=g++-7
export CPP=cpp-7

echo "-------------------------------------------------------------------------"

echo "FC  = ${FC}"
echo "F90 = ${F90}"
echo "F77 = ${F77}"
echo "CC  = ${CC}"
echo "CXX = ${CXX}"
echo "CPP = ${CPP}"

export cur=$PWD 

export install_path=${cur}/gcc_libs
export LD_LIBRARY_PATH=${install_path}/lib:${LD_LIBRARY_PATH}
export PATH="/usr/local/opt/make/libexec/gnubin:$PATH"

echo "All libs will installed into ${install_path}"
echo "-------------------------------------------------------------------------"
#----------------------------------------------------
#--------------      USER'S SETUP      --------------
#----------------------------------------------------

export make_check=false #true or false; someones take a long time for checking.

#
#----------------------------------------------------
#

export compile_mpich=false

export compile_zlib=false
export compile_szip=false
export compile_curl=false
export compile_hdf5=false             # Dep: zlib, szip
export compile_netcdf4c=false         # Dep: hdf5
export compile_netcdf4f=false         # Dep: netcdf-c

export compile_bzip2=false
export compile_libpng=false
export compile_jpeg=false
export compile_jasper=false           # Dep: jpeg

#---------------------------------------------------
#     provide version label for each package
#          (MAY NOT NEED TO CHANGE)
#---------------------------------------------------

export zlib_label=zlib-1.2.11
export szip_label=szip-2.1.1
export curl_label=curl-7.79.1
export hdf5_label=hdf5-1.8.22
export netcdf4c_label=netcdf-c-4.8.1
export netcdf4f_label=netcdf-fortran-4.5.2
export mpich_label=mpich-3.4.2
export jpeg_label=jpeg-9d
export libpng_label=libpng-1.2.50
export jasper_label=jasper-1.900.1
export bzip2_label=bzip2-1.0.8

#==========================STOP======================
#======================LINES BELLOW==================
#====================MAY NOT BE CHANGED==============

#----------------------------------------------------
#--------------          MPICH         --------------
#----------------------------------------------------

if [[ $compile_mpich = true ]]

then

echo 'Compile mpich ...'

if [[ ! -d ${mpich_label} ]]
then
    echo "${mpich_label} does not exist on your filesystem."
    tar -zxf ${mpich_label}.tar.gz
    echo "unzip ${mpich_label}.tar.gz ..."
fi

cd ${mpich_label}

echo "enter ${mpich_label} ..."

unset F90
unset F90FLAGS

./configure -q --prefix=${install_path}

make -s
make -s install

echo 'mpich compiled  ...'
echo "-------------------------------------------------------------------------"
cd ..

fi

#----------------------------------------------------
#--------------          ZLIB          --------------
#----------------------------------------------------

if [[ $compile_zlib = true ]]

then

#echo 'Compile zlib ...'
 
if [[ ! -d ${zlib_label} ]]
then
    echo "${zlib_label} does not exist on your filesystem."
    tar -zxf ${zlib_label}.tar.gz
    echo "unzip ${zlib_label}.tar.gz ..."
fi

cd ${zlib_label}

echo "enter ${zlib_label} ..."

./configure --prefix=${install_path}

make -s
test "$make_check" = true && make check
make -s install

echo 'zlib compiled  ...'
echo "-------------------------------------------------------------------------"
cd ..

fi

#----------------------------------------------------
#--------------          SZIP          --------------
#----------------------------------------------------

if [[ $compile_szip = true ]]

then

#echo 'Compile szip ...'

if [[ ! -d ${szip_label} ]]
then
    echo "${szip_label} does not exist on your filesystem."
    tar -zxf ${szip_label}.tar.gz
    echo "unzip ${szip_label}.tar.gz ..."
fi

cd ${szip_label}

echo "enter ${szip_label} ..."

./configure -q --prefix=${install_path}

make -s
test "$make_check" = true && make -s check
make -s install

echo 'szip compiled  ...'
echo "-------------------------------------------------------------------------"
cd ..

fi

#----------------------------------------------------
#--------------         BZIP2          --------------
#----------------------------------------------------

if [[ $compile_bzip2 = true ]]

then

#echo 'Compile bzip2 ...'

if [[ ! -d ${bzip2_label} ]]
then
    echo "${bzip2_label} does not exist on your filesystem."
    tar -zxf ${bzip2_label}.tar.gz
    echo "unzip ${bzip2_label}.tar.gz ..."
fi

cd ${bzip2_label}

echo "enter ${bzip2_label}"

make install PREFIX=${install_path} CC=${CC}

echo 'bzip2 compiled  ...'
echo "-------------------------------------------------------------------------"
cd ..

fi

#----------------------------------------------------
#--------------         LIBPNG         --------------
#----------------------------------------------------

if [[ $compile_libpng = true ]]

then

#echo 'Compile libpng ...'

if [[ ! -d ${libpng_label} ]]
then
    echo "${libpng_label} does not exist on your filesystem."
    tar -zxf ${libpng_label}.tar.gz
    echo "unzip ${libpng_label}.tar.gz ..."
fi

cd ${libpng_label}

echo "enter ${libpng_label}"

./configure --prefix=${install_path}

make -s
test "$make_check" = true && make -s check
make -s install

echo 'libpng compiled  ...'
echo "-------------------------------------------------------------------------"
cd ..

fi

#----------------------------------------------------
#--------------         LIBJPEG        --------------
#----------------------------------------------------

if [[ $compile_jpeg = true ]]

then

#echo 'Compile jpeg ...'

if [[ ! -d ${jpeg_label} ]]
then
    echo "${jpeg_label} does not exist on your filesystem."
    tar -zxf ${jpeg_label}.tar.gz
    echo "unzip ${jpeg_label}.tar.gz ..."
fi

cd ${jpeg_label}

echo "enter ${jpeg_label}"

./configure --prefix=${install_path}

make -s
test "$make_check" = true && make -s check
make -s install


echo 'jpeg compiled  ...'
echo "-------------------------------------------------------------------------"
cd ..

fi

#----------------------------------------------------
#--------------         JASPER         --------------
#----------------------------------------------------

if [[ $compile_jasper = true ]]

then

#echo 'Compile jasper ...'

if [[ ! -d ${jasper_label} ]]
then
    echo "${jasper_label} does not exist on your filesystem."
    tar -zxf ${jasper_label}.tar.gz
    echo "unzip ${jasper_label}.tar.gz ..."
fi

cd ${jasper_label}

echo "enter ${jasper_label}"

./configure --prefix=${install_path}

make -s
test "$make_check" = true && make -s check
make -s install

echo 'jasper compiled  ...'
echo "-------------------------------------------------------------------------"
cd ..

fi

#----------------------------------------------------
#--------------          HDF5          --------------
#----------------------------------------------------

if [[ $compile_hdf5 = true ]]

then

#echo 'Compile hdf5 ...'

if [[ ! -d ${hdf5_label} ]]
then
    echo "${hdf5_label} does not exist on your filesystem."
    tar -zxf ${hdf5_label}.tar.gz
    echo "unzip ${hdf5_label}.tar.gz ..."
fi

cd ${hdf5_label}

echo "enter ${hdf5_label} ..."

./configure -q --prefix=${install_path} --with-zlib=${install_path} --with-szlib=${install_path} --enable-hl --enable-shared --enable-fortran

make -s
test "$make_check" = true && make -s check
make -s install

echo 'hdf5 compiled  ...'
echo "-------------------------------------------------------------------------"
cd ..

fi

#----------------------------------------------------
#--------------        NETCDF-C        --------------
#----------------------------------------------------

if [[ $compile_netcdf4c = true ]]

then

#echo 'Compile netcdf4-c ...'

if [[ ! -d ${netcdf4c_label} ]]
then
    echo "${netcdf4c_label} does not exist on your filesystem."
    tar -zxf ${netcdf4c_label}.tar.gz
    echo "unzip ${netcdf4c_label}.tar.gz ..."
fi

cd ${netcdf4c_label}

echo "enter ${netcdf4c_label} ..."

./configure -q --prefix=${install_path} CPPFLAGS="-I${install_path}/include" LDFLAGS="-L${install_path}/lib" --enable-netcdf4 --enable-shared

make -s
test "$make_check" = true && make -s check
make -s install

echo 'netcdf4-c compiled  ...'
echo "-------------------------------------------------------------------------"
cd ..

fi

#----------------------------------------------------
#--------------     NETCDF-Fortran     --------------
#----------------------------------------------------

if [[ $compile_netcdf4f = true ]]

then

#echo 'Compile netcdf4-f ...'

if [[ ! -d ${netcdf4f_label} ]]
then
    echo "${netcdf4f_label} does not exist on your filesystem."
    tar -zxf ${netcdf4f_label}.tar.gz
    echo "unzip ${netcdf4f_label}.tar.gz ..."
fi

cd ${netcdf4f_label}

echo "enter ${netcdf4f_label} ..."

./configure -q --prefix=${install_path} CPPFLAGS="-I${install_path}/include" LDFLAGS="-L${install_path}/lib" --enable-large-file-tests

make -s
test "$make_check" = true && make -s check
make -s install

echo 'netcdf4-f compiled  ...'
echo "-------------------------------------------------------------------------"
cd ..

fi

```
