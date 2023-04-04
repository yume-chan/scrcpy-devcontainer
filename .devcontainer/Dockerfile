# syntax=docker/dockerfile:1.4
FROM mcr.microsoft.com/devcontainers/base:jammy

RUN --mount=target=/var/lib/apt/lists,type=cache,sharing=locked \
    --mount=target=/var/cache/apt,type=cache,sharing=locked \
    rm -f /etc/apt/apt.conf.d/docker-clean \
    && sudo apt update \
    && sudo apt -y install --no-install-recommends \
      ffmpeg \
      libsdl2-2.0-0 \
      adb \
      libusb-1.0-0 \
      gcc \
      make \
      git \
      p7zip-full \
      pkg-config \
      meson \
      ninja-build \
      libsdl2-dev \
      libavcodec-dev \
      libavdevice-dev \
      libavformat-dev \
      libavutil-dev \
      libusb-1.0-0-dev \
      openjdk-11-jdk \
      mingw-w64 \
      mingw-w64-tools

# Install Android SDK
# Based on https://github.com/CircleCI-Public/cimg-android/blob/main/Dockerfile.template

ENV TMP_ANDROID_HOME="/tmp/android-sdk"
ENV TMP_CMDLINE_TOOLS_ROOT="${TMP_ANDROID_HOME}/cmdline-tools/latest/bin"

RUN --mount=target=${TMP_ANDROID_HOME},type=cache,sharing=locked \
    SDK_TOOLS_URL="https://dl.google.com/android/repository/commandlinetools-linux-9123335_latest.zip" && \
    mkdir -p ${TMP_ANDROID_HOME}/cmdline-tools && \
    mkdir ${TMP_ANDROID_HOME}/platforms && \
    mkdir ${TMP_ANDROID_HOME}/ndk && \
    wget -O /tmp/cmdline-tools.zip -t 5 "${SDK_TOOLS_URL}" && \
    unzip -q /tmp/cmdline-tools.zip -d ${TMP_ANDROID_HOME}/cmdline-tools && \
    rm /tmp/cmdline-tools.zip && \
    mv ${TMP_ANDROID_HOME}/cmdline-tools/cmdline-tools ${TMP_ANDROID_HOME}/cmdline-tools/latest

RUN --mount=target=${TMP_ANDROID_HOME},type=cache,sharing=locked \
    echo y | ${TMP_CMDLINE_TOOLS_ROOT}/sdkmanager "tools" && \
    echo y | ${TMP_CMDLINE_TOOLS_ROOT}/sdkmanager "build-tools;30.0.3" && \
    echo y | ${TMP_CMDLINE_TOOLS_ROOT}/sdkmanager "platforms;android-33"

ENV ANDROID_HOME=/opt/android-sdk
ENV ANDROID_SDK_ROOT=$ANDROID_HOME
ENV PATH="${ANDROID_HOME}/emulator:${ANDROID_HOME}/cmdline-tools/latest/bin:${ANDROID_HOME}/tools:${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/platform-tools:${ANDROID_HOME}/platform-tools/bin:${PATH}"

RUN --mount=target=${TMP_ANDROID_HOME},type=cache,sharing=locked \
    cp -r ${TMP_ANDROID_HOME} ${ANDROID_SDK_ROOT}

RUN ls -al ${ANDROID_HOME}

# Cache Gradle dependencies
VOLUME /home/vscode/.gradle/
