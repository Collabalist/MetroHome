FROM mcr.microsoft.com/devcontainers/java:1-17-bullseye

# Ensure we stay as the default non-root user
USER vscode

# Set up Android SDK environment variables
ENV JAVA_HOME="/usr/local/sdkman/candidates/java/current"
ENV ANDROID_HOME="/usr/local/android-sdk"
ENV PATH="${PATH}:${ANDROID_HOME}/cmdline-tools/latest/bin:${ANDROID_HOME}/platform-tools"

# 1. Use sudo to install system packages and create the Android directory
# 2. Assign ownership of the Android directory to the vscode user
# 3. Download, extract, and set up the Android SDK tools entirely as the vscode user
RUN sudo apt-get update \
    && sudo DEBIAN_FRONTEND=noninteractive apt-get install -y unzip wget \
    && sudo mkdir -p ${ANDROID_HOME}/cmdline-tools \
    && sudo chown -R vscode:vscode ${ANDROID_HOME} \
    && wget -q https://dl.google.com/android/repository/commandlinetools-linux-10406996_latest.zip -O /tmp/cmdline-tools.zip \
    && unzip -q /tmp/cmdline-tools.zip -d ${ANDROID_HOME}/cmdline-tools \
    && mv ${ANDROID_HOME}/cmdline-tools/cmdline-tools ${ANDROID_HOME}/cmdline-tools/latest \
    && rm /tmp/cmdline-tools.zip \
    && yes | sdkmanager --licenses \
    && sdkmanager "platforms;android-34" "build-tools;34.0.0" "platform-tools"