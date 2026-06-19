# Sử dụng Ubuntu làm hệ điều hành gốc
FROM mcr.microsoft.com/devcontainers/base:ubuntu

# Thiết lập các biến môi trường cần thiết
ENV ANDROID_HOME="/opt/android-sdk"
ENV FLUTTER_HOME="/opt/flutter"
ENV PATH="$ANDROID_HOME/cmdline-tools/latest/bin:$ANDROID_HOME/platform-tools:$FLUTTER_HOME/bin:$PATH"

# Cài đặt các thư viện lõi và Java 17 (Yêu cầu mới của Android SDK)
RUN apt-get update && apt-get install -y \
    curl git unzip xz-utils zip libglu1-mesa openjdk-17-jdk wget \
    && rm -rf /var/lib/apt/lists/*

# Tải và cài đặt Android Command Line Tools
RUN mkdir -p $ANDROID_HOME/cmdline-tools \
    && wget -q https://dl.google.com/android/repository/commandlinetools-linux-10406996_latest.zip -O android_tools.zip \
    && unzip -q android_tools.zip -d $ANDROID_HOME/cmdline-tools \
    && mv $ANDROID_HOME/cmdline-tools/cmdline-tools $ANDROID_HOME/cmdline-tools/latest \
    && rm android_tools.zip

# Chấp nhận bản quyền Android và cài đặt Platform Tools, Build Tools
RUN yes | sdkmanager --licenses \
    && sdkmanager "platform-tools" "platforms;android-34" "build-tools;34.0.0"

# Tải và cài đặt Flutter SDK (bản Stable)
RUN git clone https://github.com/flutter/flutter.git -b stable $FLUTTER_HOME \
    && flutter config --no-analytics \
    && flutter config --enable-web \
    && flutter precache
