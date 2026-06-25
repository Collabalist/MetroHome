FROM mcr.microsoft.com/devcontainers/java:1-17-bullseye

# Ensure we are the default non-root user
USER vscode

# Set up Android SDK environment variables pointing to the user's home folder
ENV JAVA_HOME="/usr/local/sdkman/candidates/java/current"
ENV ANDROID_HOME="/home/vscode/android-sdk"
ENV PATH="${PATH}:${ANDROID_HOME}/cmdline-tools/latest/bin:${ANDROID_HOME}/platform-tools"

# Create the directory, download, and extract everything entirely without sudo
RUN mkdir -p ${ANDROID_HOME}/cmdline-tools \
    && wget -q https://dl.google.com/android/repository/commandlinetools-linux-10406996_latest.zip -O /tmp/cmdline-tools.zip \
    && unzip -q /tmp/cmdline-tools.zip -d ${ANDROID_HOME}/cmdline-tools \
    && mv ${ANDROID_HOME}/cmdline-tools/cmdline-tools ${ANDROID_HOME}/cmdline-tools/latest \
    && rm /tmp/cmdline-tools.zip \
    && yes | sdkmanager --licenses \
    && sdkmanager "platforms;android-34" "build-tools;34.0.0" "platform-tools"