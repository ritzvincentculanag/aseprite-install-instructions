# How to install Aseprite on Linux

> [!WARNING]
>
> I am using Linux Mint Debian Edition. If you want specific instructions for your
> system go to the official installation guide on aseprite's github page. You can
> find the link in [here](https://github.com/aseprite/aseprite/blob/main/INSTALL.md#linux-details).
> This is just my personal guide on how to install aseprite on my device so that i won't have
> to look manually for the links over the web.

## Required tools
1. Install the required dependencies.
```bash
sudo apt-get install -y g++ clang libc++-dev libc++abi-dev cmake ninja-build libx11-dev libxcursor-dev libxi-dev libgl1-mesa-dev libfontconfig1-dev
```
2. Get a version of the `aseprite-102` from the [release page](https://github.com/aseprite/skia#readme).
3. In your home directory create a folder named `deps`, and inside the `deps` folder create another fodler called `skia`.
```bash
# Go to home directory
cd ~

# Create folder called deps
mkdir deps

# Create a folder called skia inside the deps folder
cd deps
mkdir skia
```
4. Extract the downloaded `aseprite-102` to the newly created `skia` folder inside `deps`.
5. Download the source from the [release](https://github.com/aseprite/aseprite/releases)_page on aseprite's website.
6. Create a folder called `aseprite` on your home director. Inside the `aseprite` directory, create a folder called `build`.
```bash
# Go to home directory
cd ~

# Create a directory called aseprite
mkdir aseprite

# Create a folder called build inside aseprite
cd aseprite
mkdir build
```
7. Extract the downloaded aseprite sourcecode on the newly created `asprite` folder in your home directory.
8. Go to the `build` folder inside `aseprite`.
9. Run the following comamnds.
```bash
export CC=clang

export CXX=clang++

cmake \
  -DCMAKE_BUILD_TYPE=RelWithDebInfo \
  -DCMAKE_CXX_FLAGS:STRING=-stdlib=libc++ \
  -DCMAKE_EXE_LINKER_FLAGS:STRING=-stdlib=libc++ \
  -DLAF_BACKEND=skia \
  -DSKIA_DIR=$HOME/deps/skia \
  -DSKIA_LIBRARY_DIR=$HOME/deps/skia/out/Release-x64 \
  -DSKIA_LIBRARY=$HOME/deps/skia/out/Release-x64/libskia.a \
  -G Ninja \
  ..

ninja aseprite
```
