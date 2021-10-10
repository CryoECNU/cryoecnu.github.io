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

当然，如果为图方便，可以使用NETCDF-4.1.3，因为再往后的版本就是C和FORTRAN版本分开了，麻烦些。另外，要注意，gcc新版本编译NETCDF4.1.3会报错。所以建议VIC都用GCC6或者7。

这里以homebrew安装的GCC7为例，写了一个bash脚本来简化安装一些常用的库：NETCDF-C、NETCDF-Fortran、MPICH等。


```


export FC=gfortran-7
export F90=gfortran-7
export F77=gfortran-7
export CC=gcc-7
export CXX=g++-7

echo "FC  = ${FC}"
echo "F90 = ${F90}"
echo "F77 = ${F77}"
echo "CC  = ${CC}"
echo "CXX = ${CXX}"

export install_path=/Users/kangwang/Documents/compile_LIBS/gcc_libs
export LD_LIBRARY_PATH=${install_path}/lib:${LD_LIBRARY_PATH}

echo "All libs will installed into ${install_path}"

export make_check=false #true or false

export compile_zlib=true
export compile_hdf5=true
export compile_netcdf4c=true
export compile_netcdf4f=true
export compile_mpich=true
export compile_libpng=true

export zlib_label=zlib-1.2.11
export hdf5_label=hdf5-1.8.22
export netcdf4c_label=netcdf-c-4.8.1
export netcdf4f_label=netcdf-fortran-4.5.2
export mpich_label=mpich-3.3
export libpng_label=libpng-1.2.50

#==========================STOP======================
#======================LINES BELLOW==================
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

echo "enter ${zlib_label} ..."

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

if [[ $compile_netcdf4c = true ]]

then

echo 'Compile netcdf4-c ...'

if [[ ! -d ${netcdf4c_label} ]]
then
    echo "${netcdf4c_label} does not exist on your filesystem."
    tar -zxvf ${netcdf4c_label}.tar.gz
    echo "unzip ${netcdf4c_label}.tar.gz ..."
fi

cd ${netcdf4c_label}

echo "enter ${netcdf4c_label} ..."

./configure -q --prefix=${install_path} CPPFLAGS="-I${install_path}/include" LDFLAGS="-L${install_path}/lib" --enable-netcdf4 --enable-large-file-tests --disable-dap

make
test "$make_check" = true && make check
make install

echo 'netcdf4-c compiled  ...'

cd ..

fi

#----------------------------------------------------

if [[ $compile_netcdf4f = true ]]

then

echo 'Compile netcdf4-f ...'

if [[ ! -d ${netcdf4f_label} ]]
then
    echo "${netcdf4f_label} does not exist on your filesystem."
    tar -zxvf ${netcdf4f_label}.tar.gz
    echo "unzip ${netcdf4f_label}.tar.gz ..."
fi

cd ${netcdf4f_label}

echo "enter ${netcdf4f_label} ..."

./configure -q --prefix=${install_path} CPPFLAGS="-I${install_path}/include" LDFLAGS="-L${install_path}/lib" --enable-large-file-tests

make
test "$make_check" = true && make check
make install

echo 'netcdf4-f compiled  ...'

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

#----------------------------------------------------

if [[ $compile_libpng = true ]]

then

echo 'Compile libpng ...'

if [[ ! -d ${libpng_label} ]]
then
    echo "${libpng_label} does not exist on your filesystem."
    tar -zxvf ${libpng_label}.tar.gz
    echo "unzip ${libpng_label}.tar.gz ..."
fi

cd ${libpng_label}

echo "enter ${libpng_label}"

./configure --prefix=${install_path}

make
test "$make_check" = true && make check
make install

cd ..

fi

```
