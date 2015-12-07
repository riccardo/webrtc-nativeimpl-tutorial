# webrtc-nativeimpl-tutorial

**UNDER CONSTRUCTION**

This is a short collection of notes collected on attempts to run WebRTC native client implementation in Linux without a browser (This has not been successful so far).

# openwebrtc

These are some tests related to [OpenWebRTC](http://www.openwebrtc.org/).

Packages for this tutorial have been compiled on a Linux Development Machine (xUbuntu 14.0, 64 bit architecture) and on a Linux-based mini pc box (Asus EEEPC running Ubuntu server 14.04, 32-bit version).

## Step 1 - Building cerbero and openwebrtc binaries

**IMPORTANT NOTE**: this steps can be skipped by using directly the binaries attached to this project (```binaries``` folder).

On the development machine, clone repositories: 

```
git clone git@github.com:EricssonResearch/cerbero.git
git clone git@github.com:EricssonResearch/openwebrtc.git
```

Create some folder to host openwebrtc after installation phase. 
The target folder can be changed modifying ```cerbero/config/linux.cbc```. 

```
sudo mkdir -p /opt/openwebrtc-0.3
sudo chown -R $UID /opt/openwebrtc-0.3
```

Run the following commands to build.

**Note**: this is a quite long process and installs a lot of packages on your development machine.

```
cd cerbero \
&& ./cerbero-uninstalled -c config/linux.cbc fetch-package --full-reset --reset-rdeps openwebrtc \
&& ./cerbero-uninstalled -c config/linux.cbc bootstrap \
&& ./cerbero-uninstalled -c config/linux.cbc package -f openwebrtc
```

This will build for your own architecture.

It seems it should be possible to build for a different architecture by changing in the commands above the cerbero config file (```config/linux.cbc```). I guess you can for example use ```cross-lin-x86.cbc```, ```cross-lin-arm.cbc```, etc., but so far I only tested same-platform compilation on X64 and X86 architectures.

At the end of the process, a set of debian packages will be available in the cerbero folder.

## Step 2 - Installing binaries

Binaries can be installed on any debian based system matching your architecture. Unless you have built them on your own, you can find pre-built binaries in the *binaries* folder of this tutorial.

In order to install packages just run:

```
sudo dpkg -i *.deb
```

After installation is successful, openwebrtc is installed in your system.

## Step 3 - Test Server

A test server is available in the *web* folder of [EricssonResearch/openwebrtc-examples](https://github.com/EricssonResearch/openwebrtc-examples) project.
Just clone the repository and run:

```
cd openwebrtc-examples/web
nodejs channel_server.js 8080
```

You will need nodeJS on your system (```sudo aptitude install nodejs```).

If you open any browser on port 8080 you should be able to start or join a webrtc session from any browser.

## Step 4 - Launch native application

Not successfull, yet.

# webrtc-native

These are some tests related to [vmolsa/webrtc-native](https://github.com/vmolsa/webrtc-native).

Build prerequisites

```
sudo apt-get install npm
sudo apt-get install --yes build-essential python2.7 git pkg-config libnss3-dev libasound2-dev libpulse-dev libjpeg62-dev libxv-dev libgtk2.0-dev libexpat1-dev default-jdk libxtst-dev libxss-dev libpci-dev libgconf2-dev libgnome-keyring-dev libudev-dev
```

```
https://github.com/vmolsa/webrtc-native
cd webrtc-native
npm install
```


# Links

## Misc unclassified links 

- [OpenWebRTC](http://www.openwebrtc.org/)
- [OpenWebRTC on github](https://github.com/EricssonResearch/OpenWebRTC)
- [OpenWebRTC examples](https://github.com/EricssonResearch/openwebrtc-examples)
- Cerbero: the "new" official [build system](https://github.com/EricssonResearch/cerbero) with [build instructions](https://github.com/EricssonResearch/openwebrtc/wiki/Building-OpenWebRTC) and [binary releases](https://github.com/EricssonResearch/openwebrtc/releases)
- [Building Realtime Web Applications with WebRTC and Python](http://pyvideo.org/video/2938/building-realtime-web-applications-with-webrtc-an): interesting video with WebRTC basics and [server-side implementation example](https://github.com/sunu/webrtc-talk) - made with [tornado](http://www.tornadoweb.org/en/stable/).  
- [This stackoverflow post] lists a few possible alternative native implementations of interest:
	- [WebRTC native code](http://www.webrtc.org/native-code)
	- [node-webrtc](https://github.com/js-platform/node-webrtc)
- a large page of [WebRTC-related demos and resources](https://www.webrtc-experiment.com/) - code [here](https://github.com/muaz-khan/WebRTC-Experiment).	
- https://github.com/superdump/cerbero/tree/pygi/cerbero
- U4VL http://www.linux-projects.org/modules/news/
- https://www.raspberrypi.org/forums/viewtopic.php?f=63&t=99283&p=693103#p693103
- https://github.com/js-platform/node-webrtc
- https://github.com/vmolsa/webrtc-native
- http://sourcey.com/webrtc-native-to-browser-video-streaming-example/
