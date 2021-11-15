[Up](../)
# My first AppImage

I am a fan and user of [TVHeadend](https://tvheadend.org/) software. For the unfamiliar, TVHeadend is a software DVR. It has the ability to stream and record digital broadcasts and IPTV sources.

Having recently moved to Debian 11 as my daily driving operating system, I needed a client software on Linux to watch live TV and recordings from my TVHeadend server instance.

Normally, I use Kodi on my TV as a client however, I wanted something more lightweight. Supposedly you can use VLC as a client, but I could not get it to work. [Movian (Showtime)](https://movian.tv/) is the offical client developed by the original TVHeadend author.

Unfortunately this application now appears to be abandonware? I could not download Movian from the [official download link](https://movian.tv/downloads/movian) but I managed to find a mirror from [another developer](http://movian.deanbg.com/) on the project. When I went to install the application, I realised it required some very old dependencies, particularly `libwebkitgtk-1.0-0` & `libssl1.0.0`

Having come across AppImages when downloading some applications for Debian I figured it might be neat just to package the deb package with the required dependencies as an AppImage for use. [I had heard](https://www.youtube.com/watch?v=Wy63jwjpNg4), that it was relatively easy to whip up an AppImage from an existing binary.

So I had a look at the [documentation around pkg2appimage](https://docs.appimage.org/packaging-guide/converting-binary-packages/pkg2appimage.html) utility as well as some [examples recipes](https://github.com/AppImage/pkg2appimage/tree/master/recipes). Recipes are essentially a mark up file providing instructions to `pkg2appimage` utility on how to construct the AppImage.

The best way to learn the syntax for the yml mark up files is to read the documentation and have a look at few examples. Maybe even run a simple example file through the `pk2appimage` utility to get a sense of how the sausage is made.

If anyone wants to create an AppImage for Movian the recipe I constructed is below. I managed to create this AppImage successfully through mostly trial and error. I just like that it is accessible enough for a non software developer like me to be able to dabble in and get something useful out of it.

```
# Download the deb package from http://movian.deanbg.com/movian-5.0.723-deank-linux-amd64.deb
# Replace /source/path/ below with your actual file paths
# Note that I referenced an older Debian distribution below which contains the older dependencies required

app: showtime
union: true

ingredients:
  dist: jessie
  packages:
    - libwebkitgtk-1.0-0
    - libssl1.0.0
  sources:
    - deb http://archive.debian.org/debian/ jessie main
  debs:
    - /source/path/movian-5.0.723-deank-linux-amd64.deb

# Watch and note the indentation below to avoid grief

script:
  - cp /source/path/showtime.png .
```
