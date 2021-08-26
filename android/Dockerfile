FROM adoptopenjdk/openjdk11

LABEL maintainer="teregulowrustem@gmail.com"

ENV COMPILE_SDK="31"
ENV BUILD_TOOLS_VERSION 31.0.0
ENV ANDROID_SDK_ROOT "/opt/android"
ENV CMDLINE_VERSION "5.0"
ENV SDK_TOOLS "7583922"
ENV PATH $PATH:${ANDROID_SDK_ROOT}/cmdline-tools/${CMDLINE_VERSION}/bin:${ANDROID_SDK_ROOT}/platform-tools

RUN apt-get update &&  \
    apt-get install -y bash git unzip wget && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /tmp/* && \
    wget -q https://dl.google.com/android/repository/commandlinetools-linux-${SDK_TOOLS}_latest.zip -O /tmp/tools.zip && \
    mkdir -p ${ANDROID_SDK_ROOT}/cmdline-tools && \
    unzip -qq /tmp/tools.zip -d ${ANDROID_SDK_ROOT}/cmdline-tools && \
    mv ${ANDROID_SDK_ROOT}/cmdline-tools/* ${ANDROID_SDK_ROOT}/cmdline-tools/${CMDLINE_VERSION} && \
    rm -v /tmp/tools.zip && \
    mkdir -p ~/.android/ && touch ~/.android/repositories.cfg && \
    yes | sdkmanager --sdk_root=${ANDROID_SDK_ROOT} --licenses && \
    sdkmanager --sdk_root=${ANDROID_SDK_ROOT}  --install "platform-tools" && \
    sdkmanager --sdk_root="${ANDROID_SDK_ROOT}" --install "build-tools;${BUILD_TOOLS_VERSION}" "platforms;android-${COMPILE_SDK}" && \
    sdkmanager --sdk_root="${ANDROID_SDK_ROOT}" --uninstall emulator && \
    sdkmanager --update

# Set timezone
ENV TZ=Europe/Moscow
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

WORKDIR /home/android