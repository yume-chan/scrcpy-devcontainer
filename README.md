# Dev container for Scrcpy

An all-in-one developement environment for Scrcpy.

Usage:

1. Install [Docker Engine](https://docs.docker.com/engine/) or [Docker Desktop](https://docs.docker.com/desktop/).
2. Install [Visual Studio Code](https://code.visualstudio.com).
3. Install the [Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension in Visual Studio Code
4. Fork and clone this repository
1. Clone Scrcpy to `scrcpy` folder.
5. Open in Visual Studio Code, reopen in container when prompted.

On Windows, it's recommended to clone this repository in WSL, then open in Dev Container, for better file IO performance.

## What's included

* `gcc`, `make`, `ffmpeg`, `SDL`, `MinGW` and other native dependencies for building the client binaries for Linux and Windows.
* OpenJDK and Android SDK (minimal install) for building the server package.
* [C/C++](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools) extension for developing client side code.
* [Language Support for Java](https://marketplace.visualstudio.com/items?itemName=redhat.java), [Project Manager for Java](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-dependency) and [Gradle for Java](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-gradle) extensions for developing server side code.

## Known issues

1. Language Support for Java extension doesn't detect code generated from AIDL. [redhat-developer/vscode-java#2855](https://github.com/redhat-developer/vscode-java/issues/2855)
