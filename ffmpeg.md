#ffmpeg编译
1.	安装msys2
2.	pacman -S diffutils make pkg-config yasm
3.	export PATH="c:\...\CUDA\v10.1\bin\":$PATH

4.	git clone https://git.videolan.org/git/ffmpeg/nv-codec-headers.git
    cd nv-codec-headers
    make
    sudo make install PREFIX=/usr
    export PKG_CONFIG_PATH="/usr/lib/pkgconfig":$PKG_CONFIG_PATH
    
5.	./configure --enable-nonfree --enable-nvenc --enable-cuda --enable-cuvid --extra-cflags=-Ilocal/include --extra-cflags=-Inv_sdk/include --extra-ldflags=-Lnv_sdk/x64
6.	