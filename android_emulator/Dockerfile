FROM freeway/android

#inspired by Ivan Posokhov <posohof@gmail.com>
LABEL maintainer="a.zhilyaev73@gmail.com"

EXPOSE 22

ENV DEBIAN_FRONTEND noninteractive

# Install packages
RUN apt-get -qqy update && apt-get -qqy install --no-install-recommends \
    qemu-kvm \
    xvfb \
    ssh \
    libxcomposite-dev \
    openssh-server \
 && rm -rf /var/lib/apt/lists/*

# Installs Android SDK
RUN cd android && \
    yes | tools/bin/sdkmanager --licenses && \
    tools/bin/sdkmanager "emulator" "system-images;android-29;google_apis;x86_64" && \
    tools/bin/sdkmanager --update

# Add entrypoint
ADD android_emulator/entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

# Wait for emulator
HEALTHCHECK --interval=2s --timeout=40s --retries=1 \
    CMD adb wait-for-device shell 'while [[ -z $(getprop sys.boot_completed) ]]; do sleep 1; done'
