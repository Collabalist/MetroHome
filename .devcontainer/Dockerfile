FROM mcr.microsoft.com/devcontainers/java:1-17-bullseye

# Explicitly set JAVA_HOME so the Android command line tools can find it
ENV JAVA_HOME="/usr/local/sdkman/candidates/java/current"

# Set up Android SDK environment variables
ENV ANDROID_HOME="/usr/local/android-sdk"
ENV PATH="${PATH}:${ANDROID_HOME}/cmdline-tools/latest/bin:${ANDROID_HOME}/platform-tools"

# Download and install the Android Command Line Tools
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get install -y unzip wget \
    && mkdir -p ${ANDROID_HOME}/cmdline-tools \
    && wget -q https://dl.google.com/android/repository/commandlinetools-linux-10406996_latest.zip -O /tmp/cmdline-tools.zip \
    && unzip -q /tmp/cmdline-tools.zip -d ${ANDROID_HOME}/cmdline-tools \
    && mv ${ANDROID_HOME}/cmdline-tools/cmdline-tools ${ANDROID_HOME}/cmdline-tools/latest \
    && rm /tmp/cmdline-tools.zip \
    && chown -R vscode:vscode ${ANDROID_HOME}

# Switch to the vscode user to install SDK packages safely
USER vscode

# Accept all licenses and install the required Android packages
RUN yes | sdkmanager --licenses \
    && sdkmanager "platforms;android-34" "build-tools;34.0.0" "platform-tools"