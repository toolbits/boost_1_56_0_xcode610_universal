boost_1_56_0_xcode610_universal
===============================

A patch file to enable you to compile universal binary (32bits + 64bits) libraries with clang under xcode 6.1.0.<br/>
This modification is not tested completely yet.<br/>
Only compile test was done.<br/>

I'm glad if someone tests everything and posts this to boost's official.<br/>

### development environment:

o MacOS X 10.9.5<br/>
o Xcode 6.1.0<br/>
o clang = Apple LLVM version 6.0 (clang-600.0.54) (based on LLVM 3.5svn)<br/>
o boost_1_56_0<br/>



### apply a patch
### from http://github.com/toolbits/boost_1_56_0_xcode610_universal
mv [clang-darwin.jam] boost_1_56_0/.<br/>

cd boost_1_56_0<br/>

mv clang-darwin.jam tools/build/src/tools/.<br/>



### boost with clang (libc++ with C++11)
sudo rm -rf /usr/local/boost_libc++11<br/>

./bootstrap.sh --with-toolset=clang --prefix=/usr/local/boost_libc++11<br/>
./b2 toolset=clang architecture=x86 address-model=32_64 cxxflags="-std=c++11 -stdlib=libc++" linkflags="-stdlib=libc++" threading=multi pch=off<br/>
sudo ./b2 install toolset=clang architecture=x86 address-model=32_64 cxxflags="-std=c++11 -stdlib=libc++" linkflags="-stdlib=libc++" threading=multi pch=off<br/>

sudo mkdir /usr/local/boost_libc++11/lib/a<br/>
sudo mkdir /usr/local/boost_libc++11/lib/dylib<br/>
sudo mv /usr/local/boost_libc++11/lib/*.a /usr/local/boost_libc++11/lib/a/.<br/>
sudo mv /usr/local/boost_libc++11/lib/*.dylib /usr/local/boost_libc++11/lib/dylib/.<br/>



### boost with clang (libstdc++)
sudo rm -rf /usr/local/boost_libstdc++<br/>

./bootstrap.sh --prefix=/usr/local/boost_libstdc++<br/>
./b2 architecture=x86 address-model=32_64 cxxflags="-stdlib=libstdc++" linkflags="-stdlib=libstdc++" threading=multi pch=off<br/>
sudo ./b2 install architecture=x86 address-model=32_64 cxxflags="-stdlib=libstdc++" linkflags="-stdlib=libstdc++" threading=multi pch=off<br/>

sudo mkdir /usr/local/boost_libstdc++/lib/a<br/>
sudo mkdir /usr/local/boost_libstdc++/lib/dylib<br/>
sudo mv /usr/local/boost_libstdc++/lib/*.a /usr/local/boost_libstdc++/lib/a/.<br/>
sudo mv /usr/local/boost_libstdc++/lib/*.dylib /usr/local/boost_libstdc++/lib/dylib/.<br/>
