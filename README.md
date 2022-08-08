# ascii-video-player
A simple script that turns .mp4 files into ASCII characters

This is a modified version inspired by PtitGnou.

Original Code: https://github.com/PtitGnou/AsciiVideoCPP

In order to use the script you should have the .mp4 file in the same folder and when asked in the promt write the name of the files without the ".mp4". For example if the file is "video.mp4" you just need to write "video".

## Windows Build
cmake -Wno-dev -G "Visual Studio 17 2022" -Ax64 -H. -B./build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=".\build\install"
cmake --build ./build --config Release
cmake --install ./build

The result (ready to be used) is in build\install\bin folder
